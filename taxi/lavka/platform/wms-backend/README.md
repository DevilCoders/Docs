# Яндекс.Лавка

[Основная страничка на Wiki](https://wiki.yandex-team.ru/lavka/dev/platform/)

## Установка
* [MacOS](https://wiki.yandex-team.ru/lavka/dev/platform/installation-guide/#macos-guide)
* [Linux](https://wiki.yandex-team.ru/lavka/dev/platform/installation-guide/#linux-guide)

## Vagrant

Прописываем конфиг .pip

```
mkdir ~/.pip
echo "[global]
index-url = https://pypi.yandex-team.ru/simple
" > ~/.pip/pip.conf
```


[Vagrant](https://www.vagrantup.com/) - система управления виртуалкой через простой конфиг-файл.

[Инструкция по настройке](https://wiki.yandex-team.ru/lavka/dev/platform/installation-guide/vagrant/)

## Папки проекта

* _config_ - Папка с файлами конфигурации проекта
   * _requirements_ - зависимости проекта
      * _deb.txt_ - deb зависимости
      * _pip.txt_ - python зависимости
  * _main.yml_ - Основной файл конфигурации. Здесь храним все что не требуется менять часто и обязательно требуется программист. Некоторые настройки берут свои данные из переменных окружения.
  * _host-*.yaml_ - Хостовые настройки. Удобны для переопределения каких либо параметров на конкретном хосте. Например разработчика.
* _db_ - файлы миграции БД
  * _mongo_ - Миграции для MongoDB
    * _ev_ - База для сервера событий
  * _postgresql_ - Миграции для PostgreSQL
    * _main_ - Основная база (шардированная)
    * _printer_ - База принт сервера (шардированная)
* _doc_ - документация по проекту
  * _api_ - OpenAPI 3 спецификация проекта
* _dockers_ - Dokerfile-лы проекта
  * _compose_ - Файлы для запуска окружений разработчика и CI
* _mk_ - модули для Makefile
* _scripts_ - скрипты:
  * _ci_ - скрипты для CI
  * _cron_ - крон скрипты
  * _dev_  - скрипты для разработчиков
  * _prestart_scripts_ - скрипты запуска перед стартом окружений
  * _event_push.py_ - скрипт запуска сервера событий
  * _job.py_ - скрипт запуска воркера job
  * _printer.py_ - скрипт запуска сервера печати
  * _web.py_ - скрипт запуска HTTP сервера
* _stall_ - основной код проекта, разделяемые библиотеки и т.д.:
    * _api_ - файлы обработчиков запросов.
        Cтруктура аналогична документации в папке _doc_.
    * _middlewares_ - автоматически подключаемые хуки.
        Выполняться они будут в том же порядке как лежат на диске.
        Поэтому введена нумерация.
    * _clients_ - клиенты для работы с внешними сервисами
    * _daemon_ - из названия понятно :) здесь живут демоны
    * _models_ - модели проекта
    * _over_ - обработчики over над ручками
    * _scripts_ - обработчики cron
    * _sync_ - тоже для крона, но как-то исторически выросли в другую папку...
    * _web.py_ - скрипт запуска ручек
* _tests_ - тесты для pytest
* _tsql_ - шаблоны запросов к БД

## Генерация конфигов для Dorblu

Для генерации конфигов Dorblu можно использовать скрипт stall/scripts/dorblu.py:

`
dorblu.py [-h] [--config CONFIG] [--doc_root DOC_ROOT] [directory]
`

Здесь:
 - `directory` - каталог, куда будут записаны сгенерированные файлы, по
  умолчанию равен текущему каталогу;
 - `DOC_ROOT` - каталог с YAML файлами, описывающими API в формате OpenAPI,
  по умолчанию равен doc/api;
 - `CONFIG` - файл конфигурации самого скрипта,
  по умолчанию config/monitoring/dorblu.yaml.

#### Файл конфигурации скрипта

Файл конфигурации представляет собой YAML файл, которы описывает, какие файлы
dorblu нужно создать, какие URL нужно в них писать, и какие в них должны быть
доменные имена.

Каждая секция файла конфигурации описывает отдельный файл dorblu. Рассмотрим
пример файла конфигурации:

```yaml
nanny.lavka_wms_stable.yaml:
  host: wms.taxi.yandex.net
  name: lavka_wms_stable
  prefixes:
    - /api/external/
    - /api/tsd/
```
Эта конфигурация предписывает скрипту сгенерировать файл `nanny.lavka_wms_stable.yaml`
(ключ секции – это имя файла, который нужно сгенерировать).
В файле `nanny.lavka_wms_stable.yaml` поле `group.name` будет равно `lavka_wms_stable`.
Система Dorblu будет собирать статистику запросов на хост `wms.taxi.yandex.net`
по каждому из URL проекта, начинающихся с `/api/external/` или `/api/tsd/`.
Статистика по запросам POST и GET будет собираться отдельно. Помимо сбора статистики
по каждому URL, будет собираться суммарная статистика запросов на хост `wms.taxi.yandex.net`.

В сгенерированном файле URL располагаются в том же порядке, в каком их префиксы
расположены в конфигурационном файле. URL с одинаковыми префиксами располагаются в
алфавитном порядке.

В секцию можно также добавить параметр `extra`, и указать в нем путь к
файлу, который будет дописан в конец итогового YAML-файла. Например:

```yaml
nanny.lavka_wms_stable.yaml:
  host: wms.taxi.yandex.net
  name: lavka_wms_stable
  prefixes:
    - /api/external/
    - /api/tsd/
  extra: config/monitoring/extra_wms_stable.yaml
```
С помощью `extra` в YAML добавляются URL чата поддержки (/4.0/support_chat).

Чтобы проверить, нужно ли перезапускать скрипт, чтобы на графиках
появились новые ручки, можно запустить скрипт `scripts/dev/check-dorblu.sh`.

## Workflow
Добавить [бот](https://t.me/codereview_bot). Порядок выполнения задач:
0. Берем задачу у Славы через ЛС телеграм;
1. Создаем себе ветку:
  ```
  # вытягиваем изменения
  arc pull trunk

  # создаем ветку под свою задачу. Название ветки даем по коду задачи
  # из трекера (если задача там есть), например: "LAVKADEV-2222"
  arc checkout -b LAVKADEV-2222
  ```
2. Выполняем задачу;

3. Проводим статический анализа кода "линтером". Если
   настроили хуки гита, то просто пробуем закоммитить: если линтер не одобрит,
   то коммит не пройдет. Если же хуки не настроены, то перед каждым коммитом
   выполняем команду `make lint-changed`. Если линтер ставит
   10 из 10, то все хорошо. Коммитим через терминал или через PyCharm.
   Пушим командой `arc push` (или через PyCharm);

**Примечание:** если есть сомнения насчет стиля, не помним проверяли ли линтером,
то можем проверить весь проект командой `make lint`. А потом пойти
и настроить хуки аркадии, чтобы не забывать (см. раздел по установке).

4. Создаём ПР (pull-request) в Аркадии:
  ```
  arc pr create --publish
  ```
5. Когда готовы к ревью, пишем в комменты к своему ПР: `/start`;
6. Нейронки и машинные обучения выбирают того, кого призвать и призывают:
   пингуют ревьюеров в телеграме;

**Примечание:** Если речь идет о `permit`'ах, то тегаем Славу в чате телеграмма лично,
   просим проверить ПР.

8. По окончании ревью пингуют автора в телеграме.

Полезно прочитать доступные [команды](https://github.yandex-team.ru/devexp/devexp#поддерживаемые-команды), которые можно писать в комменты к ПР.

# Docker
## Docker registry
Как настроить yandex docker registry на локальной машине написано [здесь](https://wiki.yandex-team.ru/lavka/dev/platform/installation-guide/#linux-guide)

Docker registry мы используем только яндексовый. Некоторые образы из глобального docker registry мы дублируем в яндексовый с собственным префиксом.

Пример сдублированного пакета
```
registry.yandex.net/stall/nginx:1.17.5-alpine
```

### Почему яндексовый
Потому что глобальный docker registry временами здесь отваливается.
Но работает через vpn до какой-нибудь развитой страны.

### Добавить новый образ
Чтобы добавить новый образ в яндексовый docker registry, возможно нужен vpn куда-нить за рубеж. Если он сейчас действительно нужен, а у вас его нет,
пишите в телеграм `@duker33`

0. Включаем оба vpn - и яндесовый и зарубежный
1. Добавляем нужный образ в файл `config/ci/docker_images.txt`
2. Запускаем скрипт `scripts/ci/docker_fetch_images.sh`
3. Теперь новый образ можно использовать например в docker-compose файлах в CI

# Деплой

## How to Release
- **Тестинг**, Testing
  - Катим
    - Идём на вкладку с нужным pipeline своего сервиса, [например WMS front Testing](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Lavka_WMS_Customs_CustomTesting?mode=builds#all-projects)
      - "WMS Front" здесь - название сервиса
      - "Custom (Testing)" - название pipeline
    - Жмём Run в правом верхнем углу
  - Проверяем что закатилось
    - В списке со временем появится катка pipeline, [вот пример](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Lavka_WMSFrontend_Customs_CustomTesting/7821570)
    - Вверху под большим заголовком  будет ссылка на Nanny
    - По ней видно как раскатывается сервис в Няне
- **Прод**, prod, pre & stable
  - На стороне ТимСити делаем то же, что для Тестинга, только в **pipeline для прода**
    - Pipeline этот называется AutoRelease, [вот пример для WMS Front](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Lavka_WMS_Releases_AutoRelease?mode=builds#all-projects)
    - В нём жмём кнопку Run вверху справа
  - В появившейся катке под большим заголовком появится **линк на релизный тикет**
    - [Пример тикета](https://st.yandex-team.ru/TAXIREL-54835)
    - В тикете робот будет просить всякое, исполняем его желания и получим релиз
  - **Реальную сборку** кода ТимСити делает во вкладке Release, не AutoRelease
    - [Пример сборки для WMS Front](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Lavka_WMS_Internal_Release?mode=builds#all-projects)
    - Делает он её после создания релизного тикета
    - Если сборка эта упала, в тикете релиз дальше не пойдёт
    - Её можно перезапускать, она будет актуальна для того же тикета
  - **В релизном тикете** робот будет давать линки на Няню (Nanny)
    - В ней можно смотреть как код раскатывается на поды
    - Во время этой раскатки хорошо бы смотреть и на графики, если они есть

### How to Release. Skip Tests
- При релизе можно **пропустить тесты**
  - Это полезно, если катнуться надо быстро
  - А не ждать час, пока пройдут тесты
  - Которые уже катались раз в основной ветке
  - То есть полезно почти всегда на мой вкуc
- **Как пропустить тесты**, skip tests
  - Укажем `env.SKIP_TESTS=1` для катки
    - **Идём на страницу** с нужным pipeline
      - [Пример страницы](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Lavka_WMSFrontend_Customs_CustomTesting#all-projects)
    - **Жмём три точки** справа вверху рядом с кнопкой Run
    - В модалке **выбираем Parameters**
    - Добавляем `Name / Value = env.SKIP_TESTS / 1`
    - Жмём Run Build
    - Пошла катка без тестов
- **Особенность Прода** (pre, stable, AutoRelease)
  - Для Прода сборка и тесты случаются во вкладке Release, не AutoRelease
  - То есть сначала жмём **обычный Run во вкладке AutoRelease**
  - Во вкладке Release сама запускается катка с тестами
  - Останавливаем её и **перезапускаем через три точки** по инструкции выше
    - Инструкция "пропустить тесты"

## Два вида деплоя
### Через ТимСити, TeamCity
Они же **релизные тикеты**.

Чтобы получить представление о том как работает деплой через ТимСити, можно почитать [как его настроить](https://wiki.yandex-team.ru/taxi/backend/automatization/how-to-migrate-to-teamcity/). Не самый продуктивный метод, но другого пока нет.

### Через deploy.mk
Этот метод используем только там, где нет деплоя через ТимСити. Обычно это новые сервисы, где его ещё не успели настроить. Например Make-рецепт `deploy-testing-wms-ui` (это пример, конкретно этот рецепт не запускаем)

### Статика на AWS S3
Некоторые сервисы, например lavka-fe и lavka-picker хостят фронтовую статику на S3.
При деплое собранная статика загружается в S3. Для загрузки нужны aws_acccess_key_id + aws_secret_access_key.

Штатно всё это происходит в тимсити pipeline, он содержит ключи и скрипты загрузки и нам ни о чём не надо беспокоиться.  Но в случае использования deploy.mk нам нужно корректно положить ключи.

#### Ключи для AWS
Если что-то пошло  не так, сразу проверяем пару ключей aws_acccess_key_id + aws_secret_access_key. Ключи разные для разных сервисов.

Кроме того, aws_access_key_id определяет в какой контекст мы попадаем при подключении к серву S3. Поэтому при любой ошибке со стороны серва S3, например "wrong bucket", сразу проверяем от того ли сервиса у нас aws_access_key_id.

# Запуск среды

## Базовый пример
Запускаем любой из трёх сервисов изолированно в докере и в полной обвязке
```
make run-back-docker

make run-front-docker

make run-picker-docker
```

## Make-рецепты для запуска окружения

Чистим окружение
```
make down
```

### Use cases
**Для фронтов**. Типичный запуск на локальной тачке
```
# чистим окружение и стартуем бэк_серв
make down start_back_local

# готовим фронт
cd modules/lavka_fe
yarn install
yarn start

# стартуем рецепты с cypress
yarn cy:open
```
Окружение готово к работе с cypress. [Подробности о cypress](https://a.yandex-team.ru/projects/lavkawms/code/taxi/lavka/platform/wms-front/cypress?dir=taxi%2Flavka%2Fplatform%2Fwms-backend)

**Для бэков**. Типичный запуск на локальной тачке
```
# чистим окружение, говим бэк
make down cook_back_local

# проверяем что бэк стартанул корректно
make check_back_local
```


### Local way details
Работа на хост-машине.

Для бэков. Готовим простой бэкэнд. Запуск только основных баз и миграций
```
make simple_back_local

# aliases: simple_back_l, simple_back
```

Для бэков. Готовим бэкэнд. Запуск всех баз и миграций
```
make cook_back_local

# aliases: cook_back_l, cook_back
```

Для фронтов. Стартуем бэкэнд серв для работы с фронтом
```
make start_back_local

# aliases: start_back_l, start_back
```
Это `make start_back_docker` с засеванием фикстур в базу. Фикстуры - это файл lavka_users. Из него можно брать логины и токены для работы с фронтом с локальной тачки без тестов.

### Docker way details
Работа внутри докер-контейнеров для любителей изоляции на локальной машине. CI использует эти рецепты.

Остановить все контейнеры проекта
```
make stop_docker
```

Старт любого из трёх докер_сервисов. Старт с зависимостями: фронт стартует бэк, например
```
make start_back_docker

make start_front_docker

make start_picker_docker
````

Запуск тестов любого из трёх сервисов. Сервис должен быть запущен через `make start_*_docker`
```
make test_back_docker

make test_front_docker

make test_picker_docker
````

Пример использования
```
make down start_front_docker test_front_docker
```

Пример с алиасами
```
make down start_front_d test_front_d
```

### Arcadia
* Документация
  * https://docs.yandex-team.ru/arc/
* Дока для секции ревью
  * https://docs.yandex-team.ru/arcanum/pr/review_configuration

#### a.yaml config
* sevice - это имя сервиса для отображения
* title - имя сервиса в ABC
  * Если указано неверно, это некритично
  * Но и пустым быть не может
* В списке arcanum.auto_merge.requirements
  * Три сборки в ТимСити
      * type - id самого pipeline
      * alias - как будет подписана проверка в PR UI
      * disabling_policy - можно ли отключать эту сборку
      * branch_prefix - на изменения в какой папке триггерится проверка
  * Значения полей
    * comment_issues_closed - говорить о наличии незакрытых тикетов
    * approved - нужен ОК одного ревьюера
      * ок самому себе не считать
    * st_issue_linked - нужно привязать тикет

# Dev Tools
## Linter
Линтнуть staged изменения
```
make lint-staged
```

Линтнуть все изменения: staged, working tree, untracked
```
make lint-changed
```
