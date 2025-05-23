# Clownductor

`Like conductor but with a twist.` (c) @oxcd8o

Клоундуктор на самом деле является системой из немного разрозненных сервисов:
* clownductor - главный за всех, также отвечает за создание всех внешних сущностей (или инициирует процесс их создание в других сервисах/системах)
* clowny-alert-manager - отвечает за генерацию мониторингов на основе конфигов в репозитории [infra-cfg-juggler](https://github.yandex-team.ru/taxi/infra-cfg-juggler)
* clowny-balancer - отвечает за создание L7 балансеров
* clowny-perforator - отвечает за tvm правила
* strongbox - отвечает за секреты сервисов и их доставку на машинки
* task-processor - наша реализация state машины, позволяет запускать длительные операции (рецепты)

Сюда же можно дополнительно подложить следующие сервисы, необходимые для эксплуатации:
* dorblu - анализирует, агрегирует (на основе конфигов в репозитории [infra-cfg-graphs](https://github.yandex-team.ru/taxi/infra-cfg-graphs)) и отправляет в соломон и графит (deprecated) метрики работы веб-сервисов (тайминги, rps, коды ответов, распределение трафика по датацентрам)
* duty (deprecated?) - интерфейс для заведения и управления дежурными группами разработки, сейчас все дежурства переезжают в abc, так что инструмент по большей части не развивается.

Также сбоку лежит базовый образ rtc-baseimage и сервис-болванка rtc-stub (используется для раскатки базового образа свежесозданного сервиса).
Основными их контрибуторами являются в основном админы.

## Важно
Клоун является системой управления над всеми сервисами такси, лавки и еды (пока, список может разрастаться).
Стоит не забывать, что любые правки в сервис могут сломать такие вещи как релизный цикл, создание новых сервисов, аудитные механизмы и т.д.

Клоун взаимодействует с большим числом внешних (для такси) сервисов. Их поведение и особенности использования не всегда очевидны.

## Замечания по добавлению новых фич
**ВСЕ** новые фичи должны выкатываться под конфигом и выключены.
Если вы кардинально меняете поведение какого либо места, необходимо писать код так, что бы при включении конфига, новый метод бесшовно фолбечился на старый метод работы.
Для **выключения** старого поведения также необходимо использовать конфиг.
Базовый конфиг с фичами - [CLOWNDUCTOR_FEATURES](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/CLOWNDUCTOR_FEATURES) - представляет собой плоский словарь, т.е. ключами являются некие конкретные фичи, а значениями булево значение.
Но если вы создаёте сложную функциональность, для которой подобной плоской структуры будет недостаточно — заводите новый конфиг. Полезно в конфиге уметь включать/выключать определённый функционал по проектам и/или по сервисам.
Чаще всего для новой крон таски **нужно** заводить новый конфиг с гибкой настройкой каждого шага выполнения таски.

## Замечания по редактирования рецепта
Стоит всегда помнить, что у стейбла есть два окружения: престейбл и стейбл.
Когда вы катите новый код — он в начале оказывается в пре и только после этого оказывается в стейбл.
Это накладывает большие ограничения на редактирование рецепта — правки должны быть совместимы для обеих версий кода.
Что это значит: допустим мы выкатываем рецепт с новым кубиком, тогда после того как он отработал на пре, при продолжении обработки рецепта в стейбле не должно ничего кардинально поменяться.

Основные ошибки:
* изменение маппингов в рецепте без сохранения обратной совместимости (к примеру удаление выходных параметров, добавление обязательных параметров)
* добавление совершенно нового кубика в рецепт — тогда, в случае если джоба была создана из престейбла, в стейбле ТП будет падать, т.к. он ничего не знает о новом кубике
* забыть описать в рецепте в маппингах входные параметры кубика, т.к. они оказались одноимёнными

Удобно, если вы делаете мега фичу, для которой требуется несколько рецептов — делать на каждый рецепт отдельный ПР.

Стараться не делать слишком большие рецепты, и не усердствовать с ветвлениями. К примеру сейчас рецепт деплоя в прод через чур разросся из-за резолва диффа - он на самом деле хороший пример для выселения в отдельный рецепт, но делать это надо **крайне** аккуратно.
Также сильно ветвить рецепт не стоит — следить за всеми связями бывает сложно, но когда делаете ветку **обязательно** привязывайте джобу к сервису и бранчу.

### Замечания по тестированию
1. **ЗАПРЕЩЕНО** использование встроенного таск процессора и asyncio.sleep для теста рецепта
2. необходимо использовать фикстру `task_processor` из либы `task-processor-lib`
3. все кубики для тестирования обязаны предоставлять метод `output_parameters`, в котором описываются все выходные параметры и кубик **обязан** возвращать в пейлоаде все включи из этого списка
4. стоит избегать ситуаций, когда кубик может "засыпать" при определённых условиях
5. имя своего рецепта необходимо добавить в [список](https://github.yandex-team.ru/taxi/backend-py3/blob/32d4defd25531eab7bbbc97dcfaca5056075c446/services/clownductor/test_clownductor/conftest.py#L687)
6. на тест рецепта повесить несколько обязательных фикстур: `@pytest.mark.usefixtures('mock_internal_tp')`, `@pytest.mark.features_off('task_processor_enabled')` - первая мокает внутренних таск-процессор так, что он создаёт джобы внутри библиотечного, а вторая выключает внутренний таск-процессор
7. для проверки джобы надо:
    1. получить job_id созданной джобы
    2. через метод find_job получить объект джобы
    3. запустить джобу через фикстуру run_job_common
8. не рекомендуется проверять кейсы, когда кубик может "уснуть"

Более подробно про саму библиотеку для тестирования можно почитать [ТУТ](https://wiki.yandex-team.ru/taxi/backend/architecture/task-processor/#metodtestirovanijareceptov)

## Замечания по редактированию кубиков
* Всегда добавляйте описание в doc string кубика
* Если модуль стал слишком большим (больше 1к строк) стоит подумать над распиливанием модуля на несколько
* Кубик должен быть максимально коротким (желательно, чтобы была только одна изменяющая операция на весь кубик)
* Кубик должен быть идемпотентным — их необходимо проектировать так, чтобы ретраи обрабатывались корректно (к примеру кубик создания новой сущности в няне должен проверять её наличие)
* Описывайте **все** параметры кубика, в том числе выходные

## Подключенные библиотеки
Клиентские:
* client-startrek
* yp-api
* abc-api
* staff-api
* awacs-api
* dns-api
* l3mgr-api
* nanny
* nanny-yp
* client-approvals
* client-github
* duty
* hejmdal

## Подключенные плагины
Клиентские:
- strongbox
- dispenser
- kibana
- task-processor
- clowny-perforator
- clowny-balancer
- statistics

## Внутренние плагины
Апишки:
* abc_nonofficial_api
* abk_configs
* conductor_api
* golovan
* grafana_api
* lenta_api
* login_api
* mdb_api
* puncher_api
* solomon_api
* yav_api

Хелперы:
* locks - плагин хелпер для работы с локами в клоуне (используется в рецептах)
* disk_profiles - плагин хелпер для работы с дисковыми профилями
* roles - плагин генератор, для генерации ролей из yaml описания
* service_manager - плагин хелпер, содержащий в себе основные абстракции по работе с сущностями клоуна

## Алерты
На данный момент включена проверка активности [ядра](https://solomon.yandex-team.ru/admin/projects/taxi/alerts/6d92dccb05a9279ce9c415b00ab951e6f5b95aa57fe48a535880b9d4e4d5bb98).
[wiki](https://wiki.yandex-team.ru/taxi/backend/architecture/clownductor/#alerty)
Данный алерт проверяет наличие метрик с каждого экземпляра сервиса на подах каждого ДЦ.
Падение ядра означает отсутствие метрик.
Окно проверки ровно 5 минутам с делеем в 10 сек. Варнинг сработает при падении трети от всего количества ядер т.е. реаллокация и ученьки не влияют на проверку, при этом сервис должен вывозить нагрузку без трети ядер.
Крит при наличии всего 4-х активных ядер.
Нотификация поступает в [чат](https://t.me/joinchat/Fp2Uq0wauw0KmLc6W1TEkA).
