# Вычислительные квоты

Sandbox имеет встроенную систему **квотирования** вычислительных ресурсов (ядер, памяти, диска), позволяющую гарантировать, что каждая команда получает все доступные ей мощности. Квота всегда привязана к [группе](groups.md).

Квоты и их расход по группам можно смотреть на [дашборде в Графане](https://grafana.yandex-team.ru/d/000015873/sandbox-quota-consumption-production?).

Распределение квот между группами одного сервиса, а также подъём и спуск квот выполняются на вкладке "Квоты" на странице ABC-сервиса ([документация](https://wiki.yandex-team.ru/intranet/abc/docs/quotas)).

![Квота](img/quota-info.png "Квота" =500x)

## Quota Points { #quota-points }

Квота измеряется в т.н. **quota points** (QP):

    1 секунда работы x (1 CPU или N ГБ памяти) = 10 µQP

Здесь N зависит от соотношения `RAM / cores` на хосте, который исполняет задачу. Обычно N находится в диапазоне от 4 до 8.

Для оценки того, сколько QP вам требуется, подходит следующий расчёт.
Если задача не менее 12 часов подряд монопольно выполняется на хосте с 32 ядрами, то её потребление может быть вычислено так:

    32 ядра * 3600 секунд * 12 часов * 10µQP ≈ 13.8 QP

Временной интервал 12 часов используется из-за того, что квота рассчитывается именно на 12-часовом скользящем  окне.

{% cut "Детали алгоритма" %}

Алгоритм подсчета основан на DRF ([подробнее об этом семействе алгоритмов уже рассказывали разработчики YT](https://acid.at.yandex-team.ru/27/)). В качестве основы для расчетов выступает доминанта от используемых задачей ресурсов CPU и RAM в единицу времени. Здесь важно заметить, что учитываются именно реально используемые, а не заявленные задачей минимальные требования к этим ресурсам.

Как уже говорилось, рассчёт потребления ресурсов выполняется на 12-часовом скользящем окне.
При запуске задачи мы учитываем прогнозируемое время её исполнения (параметр `kill_timeout`), и засчитываем часть этого потребления авансом.

Рассмотрим расчёт потребления на примере.
Предположим следующее: группа SANDBOX хочет запустить задачу с параметром `kill_timeout`, равным, для удобства, 55 часам. В этом случае произойдёт следующее:

1. При добавлении задачи в очередь производится прогноз времени её исполнения по формуле `kill_timeout / phi`. Здесь `phi` — это золотое сечение. Соответственно, для нашего примера прогнозируемое время исполнения будет `55 часов / (55/34) = 34 часа`.
2. Пока в очереди задач существуют группы с меньшим отношением суммы фактического и будущего потребления к их квоте, задача группы SANDBOX будет стоять в очереди (статус `ENQUEUED`).
3. Для каждого хоста известно соотношение `host_ratio = host_RAM / host_cores`. Когда задача извлекается из очереди и отдаётся на хост (переходит в статус `ASSIGNED`), для неё определяется доминантный ресурс на этом хосте `dominant = max(required_cores, ceil(required_RAM / host_ratio))`.
4. К будущему потреблению SANDBOX добавляется `kill_timeout / phi * dominant * 10` µQP.
5. Всё время, пока задача исполняется, диспетчер очереди добавляет к прошлому и вычитает из будущего потребления SANDBOX число, пропорциональное `dominant` и проходящему времени.
6. Когда задача закончила исполняться, она больше не учитывается в будущем потреблении.

Таким образом, остаток квоты группы зависит как от прошлого потребления за 12 часов, так и от прогнозируемого (будущего) потребления.
При этом:
- Выполненная задача продолжит полностью учитываться в квоте, пока не пройдёт 12 часов с момента её запуска. С этого момента она начнёт «выливаться» из прошлого потребления вплоть до момента завершения + 12 часов;
- `kill_timeout` задач выгодно держать близким к реальному времени их работы — так они будут меньше влиять на прогнозируемое потребление и тратить меньше квоты.

{% endcut %}

Формулы для расчётов:
* `1 core = 0.432 QP`
* `1 QP ≈ 2.315 cores`

## Квота по умолчанию { #default-quota }

По умолчанию, любой новой группе начисляется квота **2.472 QP**. Это соответствует примерно 2 часам времени одного 32-ядерного сервера на 12-часовом окне. Этого должно хватить для запуска первых задач и понимания того, сколько квоты на самом деле надо.

Квота по умолчанию не отображается на странице ABC-сервиса. Если требуется передать в группу вычислительные ресурсы, сначала потребуется [создать аккаунт в ABC](#create-account).

## Управление квотами в интерфейсе ABC { #manage-quotas }
### Создание аккаунта { #create-account }
Если группа привязана к ABC-сервису, но не отображается в интерфейсе ABC среди аккаунтов в провайдере Sandbox, то этот аккаунт надо создать.

Для этого:
- Зайти на вкладку `Квоты` на странице ABC-сервиса.
- Выбрать провайдер `Sandbox`.
Если в таблице нет провайдера `Sandbox`, необходимо нажать на область с фолдером "default" и в сайдбаре справа нажать `Создать аккаунт`, после выбрать провайдер `Sandbox`.
- Нажать `Создать аккаунт`.
- Указать `Название` в точности совпадающее с именем группы. Если указать отличное от этого имя, то создастся новая группа в Sandbox.
- Пространство аккаунтов - `вычислительный кластер`.

![Передать квоту](img/abc-create-account-provider-sandbox.png "Передать квоту" =500x)

### Передать квоту в интерфейсе ABC { #pass-quota }
Дальше передача квоты в сам аккаунт делается просто:
- Нажать `Изменить квоту`
- `Добавить ресурс` при необходимости
- В `Спущено` указать целевое значение в ядрах (`core`) и подтвердить

## Иерархия { #structure }
Sandbox-группы могут быть организованы в двухуровневую иерархию. В такой схеме квота записывается на корневую группу, и распределяется в дочерних группах в пропорциях, указанных в их свойствах.
В этом случае при перерасходовании квоты группа будет использовать квоту родительской группы (и квоту своих соседей, соответственно). Это может позволить сильнее перерасходовать квоту одной группой за счёт большой общей квоты.

При такой организации квоты, необходимо чтобы:
* Родительская группа была с нулевой квотой.
* В родительской группе не запускались задачи, поскольку в такой конфигурации родительская группа будет иметь низший приоритет по отношению в дочерним.
* Желательно, чтобы группы были привязаны к одному АБЦ сервису

Эта функциональность недоступна для управления через API, но может быть организована [по запросу в общем порядке](https://wiki.yandex-team.ru/sandbox/#support).


## Что делать, если квоты не хватает { #lack-of-quota }

Если нехватка временная и хочется подтолкнуть небольшое количество задач, то это [можно сделать увеличением приоритета](#quota-on-credit).

Если нехватка квоты проявляется регулярно, то стоит сделать что-то из следующего:
* Договоритесь с другой командой о передаче части их квоты в вашу группу;
* Закажите квоту во время общего заказа ресурсов в компании (происходит раз в год);
* [Передайте собственные сервера в Sandbox](#add-hosts);
* [Оптимизируйте потребление ресурсов задачами](#optimize).

При наличии достаточного количества ресурсов в резерве Sandbox возможно получить квоту авансом.
Для это надо предоставить тикет на соответствующий заказ ресурсов.

## Временное увеличение квоты (запуск в кредит) { #quota-on-credit }
В случае, если нужно форсировать запуск задачи, можно поднять ей приоритет до **USER**. Такие задачи запускаются «в кредит»: они стоят в дополнительной очереди, откуда вынимаются при следующих условиях:
- **USER:LOW**: `r >= -q * 1/3`;
- **USER:NORMAL**: `r >= -q * 2/3`;
- **USER:HIGH**: `r >= -q`.

Здесь `r` и `q` — остаток квоты и сама квота, соответственно.

Нужно понимать, что такой запуск задач пропорционально отдалит начало выполнения задач, уже ожидающих в очереди в других классах приоритетов.

## Передача физических хостов { #add-hosts }

Для передачи железных серверов в Sandbox они должны удовлетворять следующим требованиям:

* **Процессор:** любой современный от Intel (E5-2650/2660/...), кроме E5645);
* **RAM**: 128Gb и выше;
* **Датацентр**: любой, кроме Ивантеевки и Мытищ.

Для передачи серверов в Sandbox нужно создать задачу через [форму](https://st.yandex-team.ru/createTicket?queue=SANDBOX&_form=49717) и указать инвентарные номера серверов. Перед тем, как создавать заявку проверьте, что хосты:

* переданы в [Bot'е](https://bot.yandex-team.ru/) в проект `Search Portal -> Infrastructure (VS) -> Технологии разработки -> Sandbox`;
* удалены из вашего проекта в [Wall-E](https://wall-e.yandex-team.ru/);
* удалены из [Conductor](https://c.yandex-team.ru/);
* удалены из [GenCfg](https://gencfg.yandex-team.ru/);
* перевешены на VLAN 542 или 999 в [Racktables](https://racktables.yandex-team.ru/).

## Оптимизация потребления квоты { #optimize }

Если потребление вашей квоты приближается к 100% или стабильно больше этого значения, это сигнал к тому, чтобы увеличить квоту или задуматься об оптимизации потребления.
Возможные способы оптимизации потребления:

1. **Запускать задачи на [мультислотовых агентах](agents.md#slots).**
    Если ваша задача для своей работы не требует большого железного сервера в единоличный доступ,
    то переезд в контейнер небольшого размера может существенно сэкономить квоту.
2. **Сократить требования задачи.**
    Стоит убедиться, что задаче действительно нужно объявленное количество ядер и памяти.

    Для того чтобы оценить реальное потребление ресурсов, можно открыть вкладку **Other > Hardware** на странице задачи:
    ![Потребление ресурсов задачей](img/quota-hardware-page.png "Потребление ресурсов задачей")

    {% note info "" %}

    Потребление ресурсов доступно только при запуске на LXC-хостах.

    {% endnote %}

    Также в логах выполнения задачи сохраняется файл `atop.out`, который содержит много информации о реальном потреблении ресурсов хоста процессами задачи.
    Для чтения этого лога может понадобиться [специальный бинарник atop](tasks.md#atop-log).
