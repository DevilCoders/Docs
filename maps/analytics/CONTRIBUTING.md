# Руководство по разработке

## Общие правила
* вся работа ведется на выделенных виртуальных серверах [Jupyter](https://wiki.yandex-team.ru/jupyter/)
* основным редактором для работы является [PyCharm](https://www.jetbrains.com/pycharm/), дополнительным [VS Code](https://code.visualstudio.com/) 
* генерация логов и датасетов для продакшена должны всегда производиться от имени робота [robot-maps-analytics@](https://staff.yandex-team.ru/robot-maps-analytics)

## Разграничение прав доступа
* все права выдаются только на abc-сервис [maps-analytics](https://abc.yandex-team.ru/services/maps-analytics)
* в YT по адресу `arcadia/maps/analytics` права на создание новых папок есть только у разработчиков инфраструктуры, для экспериментов и временных решений у всех есть права на создание папок в `arcadia/maps/analytics/tmp` (создаем папку со своим логином и работаем в ней)
* для нирваны созданы следующие роли:
  * [maps-analytics](https://nirvana.yandex-team.ru/roles/maps-analytics) — для доступа к директориям
  * [nirvana.flowchart.maps-analytics](https://nirvana.yandex-team.ru/roles/nirvana.flowchart.maps-analytics) — для управления графами
  * [nirvana.operation.maps-analytics](https://nirvana.yandex-team.ru/roles/nirvana.operation.maps-analytics) — для управления операциями
* все секреты храним в [секретнице](https://yav.yandex-team.ru/), для всех секретов выставляем теги `maps` и `maps-analytics`, доступ на редактирование выдаем для [maps-analytics](https://abc.yandex-team.ru/services/maps-analytics) (скоупы Аналитика и Разработка)

К сожалению, не все права доступа можно выдать abc-сервису, поэтому некоторые надо **получить персонально**.
| Сущность | Как получить доступ |
|---|---|
| Квота [geo-analytics](https://dispenser.yandex-team.ru/nirvana/projects/geo-analytics) для запуска графов в Нирване | Написать одному из ответственных добавить себя в участники |
| Участник проекта [maps-analytics](https://nirvana.yandex-team.ru/project/maps-analytics) | Написать одному из ответственных добавить себя в участники |


## Используемые библиотеки и инструменты
* [Консольный клиент YT](https://yt.yandex-team.ru/docs/api/cli/cli)
* [Библиотека Nile](https://doc.yandex-team.ru/stat/nile/) и [Консольный клиент Nile](https://clubs.at.yandex-team.ru/statistics/943) — описание и запуск расчётов на mapreduce
* [Библиотека QB2](https://doc.yandex-team.ru/stat/qb2/core/) — набор хелперов для работы с логами
* [Lama](tools/lama) — утилита для управления конфигурациями Реактора и Нирваны

## Настройка окружения

Концепция рабочего окружения – редактируем, коммитим локально на ноутбуке, а запускаем расчеты на удаленном сервере в screen/tmux. Таким образом писать код можно и без интернета, а запустив долгий расчет, закрыть ноутбук и пойти на встречу.

### 1. Создание выделенного виртуального сервера [Jupyter](https://wiki.yandex-team.ru/jupyter)
* создайте виртуальный сервер по [официальной инструкции](https://wiki.yandex-team.ru/jupyter/docs)
* все аналитики и разработчики инфраструктуры аналитики используют сервисную квот из [maps-analytics](https://abc.yandex-team.ru/services/maps-analytics), остальные — `JupyterCloud`
* если вам для рабочих нужд нужна повышенная квота — [запросите](https://forms.yandex-team.ru/surveys/49959/)
* добавьте в `~/.ssh/config` шорткат для своего виртуального сервера
```
$ tee -a ~/.ssh/config << END
Host jupyter
ForwardAgent yes
User {{login}}
HostName jupyter-cloud-{{login}}.{{datacenter}}.yp-c.yandex.net
END
$ ssh jupyter # соединиться по ssh
```

После создания машинки вы получите выделенный сервер с настроенным `Jupyter Notebook` и `Jupyter Lab`.

Если долго не заходить на виртуальную машину `Jupyter` (больше 7 дней), то она остановится. Нужно в интерфейсе опять ее запустить

### 2. Клонирование [Аркадии](https://wiki.yandex-team.ru/arcadia/)
#### Локально
* [установите себе arc и смонтируйте аркадии](https://doc.yandex-team.ru/arc/setup/arc/install.html) локально
* выполните следующий код по первоначальной настройке:
```
$ echo '
if [ -d ~/bin ] ; then
    PATH=~/bin:"${PATH}"
fi' >> ~/.profile
$ mkdir ~/bin
$ source ~/.profile
$ ln -sf ~/arc/arcadia/ya ~/bin/ya
$ ya make ~/arcadia/maps/analytics/tools/lama/bin
$ ln -sf ~/arcadia/maps/analytics/tools/lama/bin/lama ~/bin/lama
```
#### На сервере
* зайдите на [Jupyter](https://wiki.yandex-team.ru/jupyter/) и скопируйте адрес виртуального сервера (имеет вид `jupyter-cloud-{{login}}.{{datacenter}}.yp-c.yandex.net`)
* зайдите на на сервер по `ssh`
* смонтируйте [файловую структуру для arc](https://doc.yandex-team.ru/arc/setup/arc/install.html) на сервере
* выполните тот же код, что выполняли локально

В итоге у вас должно получить две копии аркадии: локальная и на виртуальном сервере. Периодически запускаем команду `arc pull` в корне аркадии локально и на сервере, так будут синхронизованы файлы Аркадии.

Также рекомендуется создать себе `~/arc/Makefile` следующего содержания:
```
mount:
    arc mount -m arcadia/ -S store/

unmount:
    arc unmount arcadia
```
Это позволит простыми командами `make mount` и `make unmount` монтировать и размонтировать аркадию.

При сборке `ya` агрессивно кеширует промежуточные результаты сборки, чтобы сокращать время повторных сборок. Это может привести к тому, что закончится место на диске и при сборке будет выдаваться сообщение `No space left on device`. Чтобы такого не произошло, рекомендуем добавить конфиг для `ya`, который будет ограничивать размер кеша.
```
$ echo '
tools_cache_size = "6GiB"
symlinks_ttl = "1h"
cache_size = "50GiB"' >> ~/.ya/ya.conf
```
Чтобы основательно почистить кеш, можно удалить старые результаты сборки с помощью следующей команды:
```
$ ya gc cache --age-limit=24 # удалит всё, что старее 24 часов
```
Более подробно об этих настройках можно прочитать в [официальной документации ya](https://docs.yandex-team.ru/ya-make/usage/ya_make/local_ya_cache#nastrojki).

Если команды выше не помогают, то можно
- удалить служебные файлы arc'а `store/.arc/objects` – [инструкция](https://wiki.yandex-team.ru/arcadia/arc/faq/#kakpochistitsluzhebnyjjkatalogstore)
- удалить `~/.ya/build/`
- удалить `~/.arc/releases/*`

### 3. Установка [PyCharm](https://www.jetbrains.com/pycharm/)
* установите себе `PyCharm Professional` последнюю версию с [официального сайта](https://www.jetbrains.com/pycharm/), либо из приложения [self-service](https://clubs.at.yandex-team.ru/helpdesk/4126); лицензию можно взять с [нашего сервера лицензией](https://wiki.yandex-team.ru/jetbrains/licenseservers/)
* откройте директорию  `/Users/<login>/arc/arcadia/maps/analytics` как проект в PyCharm
* установите [плагин для работы с аркадией](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij)
* [проверьте](https://nda.ya.ru/t/NufKskoW3W2myS), что PyCharm нашел в проекте систему контроля версий
* настройте Deployment в `PyCharm` для доставки локальных изменений на виртуальный сервер
  * `Preferences` -> `Build, Execution, Deployment` -> `Deployment` ([пример настройки](https://jing.yandex-team.ru/files/hevil/2020-06-01_14-33-13.png))
  * необходимо добавить маппинг путей должен для кода аналитики и `cofe`:
| Local Path (на вашем компьютере) | Deployment Path (на jupyter сервере) |
| ---------- | --------------- |
| `$HOME/arc/arcadia/maps/analytics` | `$HOME/arc/arcadia/maps/analytics` |
  * если при попытке тестирования соединения с виртуальным сервером получаете "host not found" или "could not connect to server", проверьте, установлена ли у вас последняя версия `PyCharm`, а также попробуйте выключить VPN и указать опцию `-Djava.net.preferIPv6Addresses=true` ([подробнее](https://intellij-support.jetbrains.com/hc/en-us/articles/207241215-Network-connectivity-issues-when-running-under-Java-1-7))
  * если при сохранении написанного кода не происходит синхронизации с виртуальным сервером, поставьте галочку `Tools` —> `Deployment` —> `Automatic Upload`
  * подробное [руководство](https://medium.com/analytics-vidhya/connecting-remote-server-via-pycharm-53414d0da93f) по настройке `PyCharm` для работы с удаленными машинами

Теперь вы готовы к работе!

## Разработка

- создавать ветки, коммитить и создавать пул-реквесты нужно локально с помощью консольной утилиты arc или через интерфейс `PyCharm` (который обращается к той же командной утилите).
- изменение файла в `PyCharm` будет автоматически синхронизовано с сервером через `Deployment`
- собирать проект и запускать расчеты нужно на сервере в [screen](https://www.gnu.org/software/screen/manual/screen.html) или [tmux](https://github.com/tmux/tmux/wiki)
- конфигурацию `Реактора` сохраняем в виде конфигов `lama.yaml` с помощью [Lama](tools/lama) (состояние репозитория [синхронизируется с Реактором каждый час](https://reactor.yandex-team.ru/browse/resolve?path=/maps/analytics/tools/lama/hourly))
— в каждом pr обязательно указываем `Assignees`, чтобы ваш pr обязательно посмотрели

### Совместная разработка
Иногда требуется внести правки в ветку на сервере, созданную другим. С ветками `users/${USER}/*` так не получится, потому что права на запись имеет только `${USER}`. Для совместного редактирования необходимо создавать ветки с префиксом `groups/maps-analytics/`.

### Дебаг бинарника Python

Во время прогонки тестов `ya make -A` есть возможность провалится в дебагер при падении теста, достаточно добавить `--pdb` в команду. По умолчанию стандартным дебагером был `pdb`, сейчас его заменили на `ipdb`. К сожалению историю и навигацию стрелочками это не починило, тут как и раньше рекомендуется использовать `rlwrap`: `rlwrap ya make -A --pdb`

Такая отладка работает и без тестов. Пишем в файле, в котором хотим поотлаживаться: `import pdb; breakpoint()`

Как пользоваться дебагером можно почитать в [статье](https://realpython.com/python-debugging-pdb/)

Установка `rlwrap`:
- Ubuntu `sudo apt-get update && sudo apt-get install -y rlwrap`
- Mac `brew install rlwrap`

### Оформление PR
- Локальная и remote ветка должны быть названы как тикет, например `geoanalytics-1111` и `users/timnosov/geoanalytics-1111`
- К каждому PR должен быть привязан тикет из стартрека. Для этого название PR берем [из трекера](https://nda.ya.ru/t/auv_Y3Vr3hEHHx)
- В описании PR должно быть краткое описание изменений

### Датасеты

**Датасеты** — это таблицы на YT построенные на основе логов и других таблиц. В них уже учтены особенности логирования сервисов, и они представлют простую для понимания таблицу над которой легко посчитать метрики.

Изменение датасета обычно состоит из следующих шагов
1. Вносим правки и смотрим на результат
    - вносите правки в расчет датасета
    - запускаете тестовый расчет датасета `make debug` на сервере из папки, где лежат `query.sql` и `Makefile`
    - в результате запускается YQL операция, которую можно найти в [интерфейсе YQL](https://yql.yandex-team.ru)
    - результат сохранится в вашу директорию на кластере `//home/maps/analytics/tmp/<login>/datasets/<dataset>/<service>/<date>`
2. Поддерживаем изменения в метрика
3. Поддерживаем изменения в репорте

### Метрики

Метрики, которые нужны и в А/Б и на дашборде, необходимо реализовывать через файлы `features.py` и `metrics.py`.
В `metrics.py` описывается метрика, которая строится на основе фичей. Пример метрики
```
{
    "name": "Конверсия в дипъюз у POI", # Название метрики
    "type": "ratio", # Тип метрики
    "key": "basemap.{agg}.deep_use.poi.cr", # Техническое название
    "values": [
        "basemap.{agg}.deep_use.poi.count$",  # Первая фича метрики – числитель для ratio метрик
        "basemap.{agg}.card_open.poi.count$"  # Вторая фича метрики – знаменатель для ratio метрик
    ]
}
```

Пример фичи – количество открытий карточек POI над датасетом `basemap`
```
{
    "key": "basemap.{agg}.card_open.poi.count$", # Техническое название
    "calc": lambda rec: 1, # Способ вычисления. Одна строчка в basemap одночает откртиые карточки POI
    "dim": {"events", "users", "sessions"}, # Типы аггрегаций, каждое значение будет подставлено в `key`
    "agg": max, # Способ аггрециий для `dim=sessions` и `dim=users`

},
```

####Про аггрегацию
Часто метрики нужно считать как сумму событий, кол-во уникальный сессий и пользователей с событием. Для настройки этого есть поля `dim` и `agg`.
- `dim=events` - считает сумму значений фичи
- `dim=session & agg=max` - считает кол-во уникальных сессий, в которых было хотя бы одно событие
- `dim=users & agg=max` - считает кол-во уникальных пользователей, в которых было хотя бы одно событие

### Репорты
[Документария по отчетам](https://a.yandex-team.ru/arc_vcs/maps/analytics/reports/README.md)

### Дашборды
Дашборды строятся в Datalens и хранятся в [maps/analytics/dashboards](https://datalens.yandex-team.ru/navigation/xwuv57zj8sjgs-dashboards)


### Реагирование на падение расчета
- Разработчик платформы вам сообщит о падении расчета со ссылкой на реакцию ([пример](https://nirvana.yandex-team.ru/reaction?id=5957837&mode=instances&selectedInstanceId=236816883))
- Вы делаете правку, мержите PR
- Переходите в реакцию и перезапускаете ее, [нажав на clone](https://nda.ya.ru/t/9cUVZ9d83W3oLL)
- В случае успешного расчета, последующие реакции запустятся автоматически
