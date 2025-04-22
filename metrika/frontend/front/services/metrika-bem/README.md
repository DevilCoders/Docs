## Быстрый старт
Подразумевается, что разработка идёт локально, потом происходит синк на `metrika-dev.haze.yandex.ru`. Если разработка происходит сразу на машинке `metrika-dev`, то некоторые пункты можно опустить

* Устанавливаем [Node version manager](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fcreationix%2Fnvm), как локально, так и на `metrika-dev`
* Устанавливаем node 8 с помощью nvm из пункта 1
* Помещаем исходники в папку `~/www/frontend` на `metrika-dev.haze.yandex.ru`
* Запускаем `npm run bootstrap -- --scope=metrika-bem` для установки зависимостей
* Запускаем `npx lerna run metrika-bem -- -- --langs=ru --bundle=common,tags` на примере Метрики
* Сайт будет доступен по адресу `frontend-${username}.metrika-dev.haze.yandex.ru`

Если нужно поднять несколько копий, то копия в папке `~/www/other` будет доступна по адресу `other-${username}.metrika-dev.haze.yandex.ru`.

## Первый запуск

Генерируем ssh ключ на своём компьютере

    ssh-keygen -t rsa # много раз Enter
    cat ~/.ssh/id_rsa.pub

Добавляем его на [Стафф](https://staff.yandex-team.ru)

Ключ со Стаффа автоматически добавится на все машинки, но это может занять время

Заходим на дев машинку

    ssh -A metrika-dev.haze.yandex.ru

Создаем директорию в домашней папке

    mkdir www && cd www

Далее преходим к [быстрый старт](#быстрый-старт)

Разработка
---------------

Разработка ведется в отдельной ветке: `${username}-${task}`, например: `gbiz-METR-31901`.

Затем оформляется PR в trunk и запускается код ревью

Параллельно с ревью идет тестирование командой QA.

После успешного ревью и тестирования задача вливается в develop, а история коммитов схлопывается до одного сообщения: `${ключ задачи}: {заголовок}`, например: `METR-31901: Обновить документацию по workflow и сборке релизов`.

## Баги в релизе

Когда в релизе появляется ошибка, создаем отдельную ветку, исправляем ошибку и делаем PR в *релизную ветку*.

После тестирования всех багов, пересобираем релиз.

Cборка релиза
---------------

Переходим в [Sandbox](https://sandbox.yandex-team.ru/tasks?type=METRIKA_FRONTEND_RELEASE)

* В поиске находим последнюю успешную задачу METRIKA_FRONTEND_RELEASE
* Кликаем по TaskId
* Клонируем задачу

Дальше два варианта:

### 1. Сборка нового релиза

* Выставить галочку "Новый релиз"
* Выставить версию из прода: [metrika.yandex.ru/version](https://metrika.yandex.ru/version)

### 2. Пересборка релиза

* Убрать галочку "Новый релиз"
* Выставить версию из ТС: [metrika-test.haze.yandex.ru/version](https://metrika-test.haze.yandex.ru/version)

После сборки/пересборки релиз выезжает на ТС и тестируется командой QA.

Если находят баги, чиним и пересобираем релиз.

Когда багов нету, через [Кондуктор](https://c.yandex-team.ru/packages/yandex-metrika-frontend/tickets) выкатываем в ПС, затем в стейбл.

После добавления в стейбл, ждем команды менеджера и раскатываем через [Rack&Roll](https://rackroll.mtrs.yandex-team.ru/rackroll/conductor/tasks/active/)

## После релиза вливаем релизную ветку в trunk

Номер сборки, который ушел в релиз, смотрим на [metrika.yandex.ru/version](https://metrika.yandex.ru/version)

## Обновление переводов

```
npx lerna run i18n --scope=metrika-bem -- -- --keysets=blocks:common:block1,blocks:common:block2
```

Зависимости и библиотеки
---------------

 * [bem-node](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fbem-node%2Fbem-node) - node.js + BEM = SPA
 * [Vow](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fdfilatov%2Fvow%2Ftree%2F0.3.x) версии 0.3. Поставляется вместе с `bem-node`
 * [bem-node-yandex](https://github.yandex-team.ru/bem-node/bem-node-yandex) - внутренние уровни переопределения для Яндекса
 * [islands](https://lego.yandex-team.ru/libs/islands/v5.8.1/) - библиотека блоков
 * [promised-models](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fbem-node%2Fpromised-models) - модели
 * [bem-promised-models](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fbem-node%2Fbem-promised-models) - обертка над моделями в терминах BEM
 * [bem-json](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fbem-node%2Fbem-json) - шаблонизатор, результат которого скармливается в [bemhtml](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fbem%2Fbem-xjst%2Ftree%2Fv7.x) для получения финальной строки html
 * [gulp](https://h.yandex-team.ru/?http%3A%2F%2Fgulpjs.com) и [enb](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fenb%2Fenb) - для сборки
 * [babel](https://h.yandex-team.ru/?https%3A%2F%2Fbabeljs.io) с [preset-es2015](https://h.yandex-team.ru/?https%3A%2F%2Fbabeljs.io%2Fdocs%2Fplugins%2Fpreset-es2015%2F) - для использования es6 синтаксиса на клиенте
 * [es6-shim](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fes-shims%2Fes6-shim) - полифиллы из es6 для использования на клиенте

Сборка умеет автоматически инлайнить картинки - необходимо добавить параметр `inline_image` в `url`. Например:

    background-image: url('icon.png?inline_image=1');

При сборке пакета такая иконка будет заинлайнена, а для `svg` еще и запущен `svgo`. При разработке этого не происходит.


## Отлаживаем серверный код:

1. После запуска сервера разработки `make watch service=metrika bundle=common langs=ru debug=1` получаем номер порта:

    chrome-devtools://devtools/remote/serve_file/@62cd277117e6f8ec53e31b1be58290a6f7ab42ef/inspector.html?experiments=true&v8only=true&ws=localhost:5859/node

    5859

2. Прокидываем ssh тунель на localhost

    ssh metrika-dev.haze.yandex.ru -N -L 5859:localhost:5859

3. Открываем в браузере:

    chrome-devtools://devtools/remote/serve_file/@62cd277117e6f8ec53e31b1be58290a6f7ab42ef/inspector.html?experiments=true&v8only=true&ws=localhost:5859/node

## Структура проекта

структура `blocks/`

 * `blocks/api` блоки, которые предоставляют интерфейс на получение данных из внешних источников (бекенда)
 * `blocks/common` обычные блоки и модели (@todo модели надо
 * `blocks/data` расширение с получением данных в блоки (используя `ctx.defer()`) или [dataTemplate](https://github.com/bem-node/bem-node#bngeneratordatatemplatedecl)
 * `blocks/inherits` расширение внешних блоков и библиотек
 * `blocks/pages` [контролеры страниц](https://github.com/bem-node/bem-node#page-blocks)
 * `blocks/utils` хелперы и легаси

## Внешние сервисы

### Api
Некоторая информация про [различные среды интерфейса/API/ClickHouse](https://wiki.yandex-team.ru/testirovanie/functesting/advtechnologies/metrika/TestStands/)

### Mongodb
Для хранения некоторых данных (дашборд, виджеты для него, отчеты пользователя) мы используем Mongodb.
Она находится на машине mtnosql01t.yandex.ru. Порт 27017. База metrika. Логин metrika. Как получить пароль, смотреть по ссылке [get_metrika_password.sh](https://github.yandex-team.ru/MetrikaAdmin/stuff/blob/master/get_metrika_password.sh).
Машина имеет только ipv6 адрес.
В проекте настройки берутся из файла /etc/metrika.xml из секции mongo-nodejs c fallback-ом в
прописаные в configs/current/mongo.json

Для того чтобы из консоли подключится к монге нужно выполнить следующую команду:

    mongo --ipv6 mtnosql01t.yandex.ru:27017/metrika -u metrika -p Пароль

Пароль, как правило, можно подсмотреть в /etc/metrika.xml в секции mongo-nodejs.

версия монги 2.6+

#### mongostat -u root -p <password>
Быстрая стата запущенного инстанса монги

Пример вывода
```
insert  query update delete getmore command flushes mapped  vsize    res faults    locked db idx miss %     qr|qw   ar|aw  netIn netOut  conn set repl       time
    20    617    296     *0     248   384|0       0   256g   517g   127g      0 metrika:1.2%          0       0|0     1|0   429k    23m  2086 rs0  PRI   11:33:05
     2    488    176     *0     196   202|0       0   256g   517g   126g      0 scheduler:6.0%          0       0|0     0|0   174k    18m  2086 rs0  PRI   11:33:06
     3    482    162     *0     209   568|0       0   256g   517g   126g      0   metrika:2.4%          0       0|0     2|0   330k    17m  2086 rs0  PRI   11:33:07
```
расшифровка:
https://docs.mongodb.com/manual/reference/program/mongostat/#fields


#### mongotop -u root -p <password>
Показывает, сколько времени тратится на чтение и запись

Пример одной записи
```
                          ns       total        read       write            2018-09-28T08:25:24
       scheduler.onetimeJobs       163ms        20ms       143ms
     visitState.viewedVisits        67ms         3ms        64ms
     quota.countersQuota3923        66ms         1ms        65ms
    metrika.userReportHitsV3        42ms        16ms        26ms
           metrika.urlParams        36ms        36ms         0ms
   visitState.selectedVisits        26ms        26ms         0ms
metrika.viewedOrderedReports        19ms        19ms         0ms
              local.oplog.rs        15ms        15ms         0ms
        quota.usersQuota3923        10ms         2ms         8ms
```
документация
https://docs.mongodb.com/manual/reference/program/mongotop/

#### Профилирование
https://docs.mongodb.com/manual/reference/method/db.setProfilingLevel/
Включить лог для медленных операций

    db.setProfilingLevel(level, options)

`level` это число 0 - 2
0 – выключено
1 - писать только те запросы, которые занимают более `slowms` миллисекунд
2 - собирать все запросы

`options` объект
`options.slowms` - запросы, которые длились дольше `slowms` миллисекунд, считаются медленными
`options.sampleRate` - по умолчанию 1

    db.getProfilingStatus()
    // { "was" : 0, "slowms" : 100 }

После этого можно посмотреть подробности про такие запросы, в том числе сколько было просканировано документов для того, чтобы найти результат и другие подробности
например

    db.system.profile.find().limit(1).pretty()


## Нагрузочное тестирование
Нужно подготовить стенд с API, это делается в полуручном режиме

1) В [sandbox](https://sandbox.yandex-team.ru) запустить таску `METRIKA_JAVA_DEVELOPMENT`. Если специфичная ветка api не нужна, то снимаем галочку "Сборка", так будет быстрее.
2) Заходим по ssh на созданный стенд, его нужно настроить:

- отредактировать /etc/metrika.xml, заменить все blackbox-mimino на blackbox-stress
- `service restart faced-metrika-yandex`
- Отредактировать mysql, чтобы faced ходил с нужным tvm id в blackbox
```
    // подключаемся к mysql
    mysql-connect;
    use conv_main;
    DELETE FROM tvm_services_by_env WHERE service_id = 239 AND environment = 'testing';
    INSERT INTO tvm_services_by_env VALUES (226, 'blackbox', 'stress test', 'testing', NOW());
    UPDATE user_quota SET multiplier = 1000000 WHERE uid = 282183929;
```
3) Заливаем наши скрипты на `metrika-ng-ps`
```
    scp -rp ./tools metrika-ng-ps.yandex.ru:/home/{USERNAME}
    scp ./GNUmakefile metrika-ng-ps.yandex.ru:/home/{USERNAME}
```
4) Заходим на `metrika-ng-ps` и подготавливаем стенд
```
    ssh -A metrika-ng-ps.yandex.ru
    sudo cp ./GNUmakefile /var/lib/yandex/yandex-metrika-frontend
    cd /var/lib/yandex/yandex-metrika-frontend
    sudo make cached-stress
    sudo service yandex-metrika-frontend restart
```
5) Генерируем патроны
Нужно взять логи nginx с тестинга (`metrika-test.haze.yandex.ru`), либо с продакшена (`metrika-ng1-1.yandex.ru`)
```
    ssh -A metrika-ng-ps.yandex.ru
    # перекидиваем логи с прода
    scp metrika-ng1-1.yandex.ru:/var/log/nginx/post/yandex-metrika-frontend-body.log ./
    # генерируем патроны из логов скриптом
    cat ./yandex-metrika-frontend-body.log | bash ./tools/load/grep.sh - | ./tools/load/genammo.py metrika-ng-ps.yandex.ru > ammo
```

Генерацией можно управлять, отредактировав файл `./tools/load/grep.sh`. Например, можно исключить некоторые страницы или ручки, вроде экспорта в pdf.

Файл `ammo` может получиться большим, можно его упаковать, так проще загружать в танк
```
    gzip -9 ammo
```
скачиваем патроны на локальную машину
```
    # мы сейчас находимся на локальной разработческой машине
    scp metrika-ng-ps.yandex.ru:/home/{YOURUSERNAME}/ammo.gz ~/Downloads
```
6) Из домашней папки запускаем nginx с кеширующим конфигом
```
    # это metrika-ng-ps
    sudo -u www-data ./tools/load/api-proxy.sh
```
7) Идём в https://lunapark.yandex-team.ru/, в верхнем меню жмём "Пострелять"

- в `Мишень` указываем `metrika-ng-ps.yandex.ru:443`
- создаём задачу в своей очереди (`METR`/`RADAR`/etc), её номер записываем в поле `Задача`
- Описываем схему нагрузки, можно через пробел. Например, `line(1, 200, 5m) const(1000, 20m)` значит, что сначала нагрузка будет равномерно возрастать с 1 до 200 rps в течении 5 минут, затем будет подана постоянная нагрузка в течении 20 минут. [Подробнее про поддерживаемые нагрузки](https://yandextank.readthedocs.io/en/latest/tutorial.html#first-steps)
- Загружаем патрон из пункта 5
- Задаём какое-нибудь осмысленное имя и описание, например `Переход на nodejs 28` и `Патроны с продакшена, без экспорта и страницы /about, у nodejs включена настройка --super-bystro`. У другой стрельбы соответственно - `Переход на nodejs 28` и `Патроны с продакшена, без экспорта и страницы /about, настройка --super-bystro выключена`
- В секции `phantom` в онлайн-редакторе внизу страницы обязательно пишем опцию `ssl: true`, иначе nginx зарежет все запросы
- Жмём `Огонь!`, ждём окончания, смотрим графики. заходим на вкладку `Мониторинг`, там можно посмотреть использование cpu и memory.
- Несколько стрельб можно наглядно сравнить в интерфейсе.

<details>
<summary>Скриншот</summary>

![alt text](https://jing.yandex-team.ru/files/rifler/2018-12-03_09_31_49.png)
</details>

## Мониторинги

Конфиги для [Monitorado](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/monitorado) лежат в `services/metrika-bem/monitorado/.monitorado.yml`.
