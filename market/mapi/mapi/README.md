# MAPI

### Описание

[Памятка разработчику](https://wiki.yandex-team.ru/market/b2c/v-team-speed/mapi-guide/)

[Памятка дежурному](https://wiki.yandex-team.ru/market/b2c/v-team-speed/mapi-guide/mapi-duty/)

### Выкладка

[Релизный пайплайн](https://tsum.yandex-team.ru/pipe/projects/mobile-blue/delivery-dashboard/mapi)

[Из ветки в тестинг](https://tsum.yandex-team.ru/pipe/projects/mobile-blue/release/new/mapi-testing-branch)

[Из ветки в престейбл](https://tsum.yandex-team.ru/pipe/projects/mobile-blue/release/new/mapi-prestable-branch)

При выкладке из ветки в поле ввода пишем arc-ветку как в PR: `users/username/branchname`


### Быстрый доступ

| Название/env              | dev                                                                                       | testing                                                                                                       | prestable                                                                                                         | production                                                                                                    |
|---------------------------|-------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| API                       | [dev](http://localhost:8080/swagger-ui.html)                                              | [тест](https://mapi.tst.vs.market.yandex.net/swagger-ui.html#/)                                               | [престейбл](https://mapi.pre.vs.market.yandex.net/swagger-ui.html#/)                                              | [прод](https://mapi.market.yandex.ru/swagger-ui.html)                                                         |
| Секретница                | [dev](https://yav.yandex-team.ru/secret/sec-01fsm5jyfec786q9nm1e3p8a90/explore/versions)  | [тест](https://yav.yandex-team.ru/secret/sec-01fq4gr3e1hppe8xgf6q0cmymp/explore/versions)                     | [престейбл](https://yav.yandex-team.ru/secret/sec-01fq4gr2a3w5gj4secnqcrnmp6/explore/versions)                    | [прод](https://yav.yandex-team.ru/secret/sec-01fq4gr23h6wryzgvgmmapdmjp/explore/versions)                     |
| RTC                       | [nanny](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_mapi)        |                                                                                                               |                                                                                                                   |                                                                                                               |
| Графана                   | [Графана](https://grafana.yandex-team.ru/d/OuyUDMT7z/market-mapi-auto-graph)              |                                                                                                               |                                                                                                                   |                                                                                                               |
| nginx                     |                                                                                           | [тестинг](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketmapi;ctype=testing;prj=market/) | [престейбл](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketmapi;ctype=prestable;prj=market/) | [прод](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketmapi;ctype=production;prj=market/) |
| proto                     |                                                                                           | [тестинг](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketmapi;ctype=testing;prj=market/) | [престейбл](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketmapi;ctype=prestable;prj=market/) | [прод](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketmapi;ctype=production;prj=market/) |
| логшаттер                 | [конфиги](https://health.market.yandex-team.ru/projects/beruapps/logshatter/configs/mapi) |                                                                                                               |                                                                                                                   |                                                                                                               |
| кликфит                   | [конфиги](https://health.market.yandex-team.ru/projects/beruapps/clickphite/configs/mapi) |                                                                                                               |                                                                                                                   |                                                                                                               |
| oauth для теста           |  |  [passport-test](https://oauth-test.yandex.ru/authorize?response_type=token&client_id=81eb4b92526d4f9494b4a87370f7c1f8)                                                                                                             |                                                                                                                   |                                                                                                               |

Графики:
- [Основной дашборд](https://monitoring.yandex-team.ru/projects/mapi/dashboards/mon8nhifbpg0pfriba22?from=now-1d&to=now&refresh=60000&p.env=production)
- [Клиентские метрики](https://monitoring.yandex-team.ru/projects/mapi/dashboards/mone6onthn5njpd3ha2m?from=now-1d&to=now&refresh=60000&p.env=production)
- [Железо+JVM для стрельб](https://monitoring.yandex-team.ru/projects/mapi/dashboards/monmakkdugs40jd0v5ht?from=now-1d&to=now&refresh=60000&p.env=production&p.host=%2A&p.dc=%2A&p.jvm_host=%2A&p.jvm_dc=-)
- [Железо](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketmapi;ctype=production;prj=market/)
- [Nginx](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketmapi;ctype=production;prj=market/)

[Локальный сваггер](http://localhost:8080/swagger-ui.html)

### Генерация проекта

Mapi работает на Java16, перед генерацией нужно установить JDK не ниже указанной версии.
JDK проще всего установить через интерфейс IDEA. При установке убедитесь, что выбираете правильную архитектуру (если работаете на М1, то нужно выбирать aarch64).

Пошаговая установка JDK:
1. Открываем IDEA, нажимаем `File => Project structure` ([скриншот](https://jing.yandex-team.ru/files/tkarpukova/First.jpg))
2. В открывшемся окне нажимаем на `+ => Download JDK` ([скриншот](https://jing.yandex-team.ru/files/tkarpukova/Second.jpg))
3. Выбираем нужную версию (16+), vendor'а (здесь внимательно смотрим на архитектуру - если вы работаете на М1, выбирайте aarch64) ([скриншот](https://jing.yandex-team.ru/files/tkarpukova/Third.jpg))

Генерация проекта для IDEA: `./generate_idea.sh ~/idea/mapi`

После генерации нужно открыть каталог `~/idea/mapi` в IDEA, и там отобразится проект + его прямые зависимости из аркадии.

Само собой, вместо `~/idea/mapi` может быть и другой путь. Он должен быть вне аркадии, это главное.

### Сборка и тесты

Сборка и прогон тестов `ya make -tt` или из IDE

Запуск конкретного теста (по имени класса или методу) `ya make -tt -F *FILTER*`

### Локальный запуск

**Важно**: для локального запуска нужно настроить переменные окружения (~/.bashrc или аналог), их нужно взять из переменной `env` в [dev-секрете](https://yav.yandex-team.ru/secret/sec-01fsm5jyfec786q9nm1e3p8a90/explore/versions)

**На mac os**: добавление в ~/.bashrc может не сработать, тогда нужно на выбор:
```
1. добавить в ~/.bash_profile (после перезагрузить ткрминал и idea)
2. добавить в environment variables в idea
3. изпользовать zsh (например такой командой "chsh -s /bin/zsh"), добавтиь в ~/.zshrc указанные выше переменные,
акркзапустить систему полностью.
```

Самый простой способ запуска приложения - через скрипт. Запустится сборка проекта + сервис запустится примерно так же, как и на стенде.

```
# простой запуск
./local-start.sh

# в режиме отладки (можно подключиться remote debug из идеи)
./local-start.sh --debug-port=6666
```

[Пример настройки конфигурации для remote debug](https://jing.yandex-team.ru/files/tkarpukova/Screen%20Shot%202022-07-04%20at%2016.28.11.png)

Также может понадобиться локальный запуск напрямую из IDE. Он быстрее, но требует более сложной настройки.

При запуске из консоли не получается подключиться к инстансу профилировщиками (возможно из-за того, что запускается в отдельной jvm)
```
Main class = ru.yandex.market.mapi.MapiLauncher
Module = mapi

java properties =
-Dlogging.config=/Users/<username>/arcadia/market/mapi/mapi/src/main/conf/local/log4j2-test.xml
-Dlog4j.configurationFile=/Users/<username>/arcadia/market/mapi/mapi/src/main/conf/local/log4j2-test.xml
-Dspring.profiles.active=local
-Dconfigs.path=/Users/<username>/arcadia/market/mapi/mapi/src/main/properties.d
-Xmx2g
-Xms2g
```

Пример настройки: https://nda.ya.ru/t/0RsM4oiJ4zCn5V

### Типичные проблемы

Проект перестал компилироваться и пишет странные ошибки.
- скорее всего это произошло после затягивания свежего транка.
- идея не узнаёт автоматически про обновление зависимостей (peerdir), и поэтому если появляются и используется новая зависимость из транка - пометит места использования сломанными
- нужно перегенерировать проект `Build / Regenerate and reload: ya ide` (нужен плагин аркадии для IDE)
- [скрин кнопки обновления проекта](https://nda.ya.ru/t/Z3bwNEkQ4zvyuW)
- после этого в правом нижнем углу нажать на кнопку "Just reload", чтобы переоткрыть проект и сбросить кэши.

При локальном запуске пишет `Could not resolve placeholder 'MAPI_TVM_SECRET_DEV' in value "${MAPI_TVM_SECRET_DEV}"`
- Нужно подтянуть параметры из секретницы, как описано выше
- если они подтянуты, но будто бы не применяются - нужно перезапустить терминал, где вызывается локальный запуск
- или перезапустить IDE, если запуск идёт через IDE

При локальном запуске через IDE пишет что-то вроде `Can't load library: /var/folders/0f/0ww8xbgs65s9pxng7n40kq1h1r3lj3/T/tvmauth_java_17347342056679645148.tmp`
- Скорее всего, вы работаете на М1, но установили jdk под intel
- Проверить можно командой `java -XshowSettings 2>&1 | grep "os.arch"` => если в os.arch указана архитектура x86_64 (но у вас М1), то нужно поставить java для M1 (архитектура aarch64)


### Логи
При локальном запуске логи пишутся в консоль. Trace уровень выключен, чтобы не сильно спамило.

Логи в rtc: `logs/mapi/mapi.log`

### Разработка

Типичная задача при разработке - добавить новую секцию+сниппет+ассемблер, или расширить уже существующие.
Как это делать - описано с примерами тут: https://wiki.yandex-team.ru/market/b2c/v-team-speed/mapi-guide/

Часто бывает полезно вызвать темплатор или фапи, чтобы проверить их ответы, и сделать это можно так.

#### Вызов темплатора

Главная
http://templator.vs.market.yandex.net:29338/tarantino/getcontextpage?device=phone&domain=ru&format=json&zoom=full&type=apps_home_screen

Параметры запроса других страних можно вытащить из контроллера. Должен меняться type, ещё возможно qualifier.

#### Вызов фапи

Импортируем в постман какой-нибудь вызов любого резолвера, например:
```
curl --location --request POST 'https://ipa.market.yandex.ru/api/v1?name=resolveStories' \
--header 'Host: ipa.market.yandex.ru' \
--header 'api-platform: IOS' \
--header 'X-Device-Type: SMARTPHONE' \
--header 'X-Platform: IOS' \
--header 'X-Region-Id: 213' \
--header 'Accept: application/json,text/plain' \
--header 'Content-Type: application/json' \
--data-raw '{
    "params": [
        {
            "pageId": "148099",
            "isLive": false,
            "isRanking": false
        }
    ]
}'
```

После этого можно поменять `name=resolveStories` на другой резолвер, а параметры вызова взять из темплатора.
Если нужно запросить под залогином - добавить заголовок `Authorization = OAuth XXXXX`, где XXXXX - это токен, полученный в сваггере мапи (важно: никем с ним не делимся!).

На всех окружениях (тестинг, престейбл, прод) используется блекбокс, работающий с продовым OAuth. Поэтому для работы на стендах токен всегда одинаковый. Подойдёт любой продовый токен, или можно сгенерить новый в сваггере или инструкцией ниже.

При локальном запуске есть нюанс:
- можно настроить разное фапи-окружение (прод, тестинг на тестовом паспорте, тестинг на мимино)
- в них нужно отправлять разный OAuth. Детали ниже

#### Вызов мапи

Проще всего вызвать через сваггер, а если параметров в нём не хватает - скопировать сгенерированный curl запроса, и импортировать в постман

### Ручное тестирование

Для выполнения запросов от лица пользователя нужно передать oauth-токен.
Токен проверяется в ЧЯ, и затем запросы в фапи и другие бекэнды идут с юзер-тикетом (где поддерживается).

В сваггере токены легко получить по кнопке "Authorize" (на стендах).

Локально работает не совсем так:
- ЧЯ тестовый, для его проверки используем токен тестового паспорта
- фапи продовый (по умолчанию), для проверки фапи используем продовый токен (не будет юзер-тикета, что учтено в клиентах + будет кидать ошибку ЧЯ в ответ)
- можно настроить тестовый фапи через заголовок запроса ```x-mapi-clients-env```
  - мимино-тестинг тоже ходит в продовый паспорт, ошибка ЧЯ будет та же, зато uid будет продовый.
  - тестинг-тестинг ходит в тестовый паспорт. Ошибки ЧЯ не будет, но будет тестовый uid, на котором возможно нет данных.

Поэтому при локальном запуске видеть в ответе ошибку `Failed to check oauth: Blackbox integration failed` - это норма.

#### Выбор окружения клиентов

Функционал позволяет переключать стенды клиентов.

Влияет на blackbox и fapi. Работает только для локального запуска и в тестинге.

Заголовок ```x-mapi-clients-env```

Возможные значения: ```test```, ```mimino```, ```prod```

Локально:

- fapi поддерживает ```prod```, ```test```, ```mimino``` (по дефолту ```prod```)
- blackbox - только тестовый

В тестинге (по дефолту ```mimino```):

- fapi поддерживает ```test```, ```mimino```
- blackbox поддерживает ```test```, ```mimino```

Инструкция получения токенов для фапи (если не хочется брать из сваггера): https://wiki.yandex-team.ru/market/beru/front/fapi-beru/kak-poluchit-token-dlja-fapi/

Пример запросов с токеном
```
curl -i  -H "X-User-Authorization: OAuth $MAPI_LOCAL_OAUTH" 'http://localhost:8080/api/screen/main?pageSize=1'
```

### Нагрузочное тестирование

В персах есть либа tank.py, с помощью которой можно строить произвольные патроны в формате танка.
Чтобы сгенерить их - нужно запустить нужный скрипт из `mapi-loadtest/src`

Пример: `python3 $ARCADIA_ROOT/market/mapi/loadtest/src/generate_main_ammo.py 100 ammo-test.txt`

Сгенерируется файл `ammo/ammo-test.txt` c 100 патронами для танка.

Может понадобиться установка следующих либ:
```
pip3 install requests
```

С готовым набором патронов идём в https://lunapark.yandex-team.ru/
И там в целом можно просто повторить какую-то старую стрельбу, добавив другие патроны, например эти:
- [в тестинг по главной](https://lunapark.yandex-team.ru/online/2956027)
- [в прод по главной](https://lunapark.yandex-team.ru/2956035)

В процессе стрельбы смотрим на графики железа (porto), а также график стрельб.
В основном, должны страдать CPU, jvm heap, jvm GC и могут начать расти ошибки рендера секций.
После стрельбы полезно посмотреть на график ошибок секций.

### Liquibase

Liquibase накатывается в пайплайне релиза. Также можно использовать скрипт `liquibase.sh`

Для использования скрипта нужно настроить переменные окружения (~/.bashrc или аналог),
их нужно взять из переменной env в [dev-секрете](https://yav.yandex-team.ru/secret/sec-01fsm5jyfec786q9nm1e3p8a90/explore/versions)

```
# доступ скорее всего будет
export MAPI_DB_PWD_TESTING=<пароль от TESTING>

# доступ сильно ограничен
export MAPI_DB_PWD_PRESTABLE=<пароль от PRESTABLE>
export MAPI_DB_PWD_PRODUCTION=<пароль от PRODUCTION>
```

Формат `./liquibase.sh <env> <command>`

- `<env>` - среда: dev, test, prod
- `<command>` - команда liquibase: updateSQL, update, ...

Пример: `./liquibase.sh dev update`

### Секретница

После изменения секрета можно накатить его через `./secmapi test/pre/prod`

Для раскатки изменений нужен проброшенный в ssh-агента сертификат.
```
# для проверки
ssh-add -l

# для добавления
ssh-add ~/.ssh/id_rsa
```

### TMS

При локальном запуске вместо полноценного планировщика кварца поднимается RAMScheduler, который работает вне кластера
(чисто локально) без использования таблиц кварца в базе данных. При этом у всех джоб вне зависимости от конфигурации
триггеров проставляется специальное крон выражение, которое, фактически, запрещает их автоматический запуск.
Для запуска в ручном режиме нужно будет использовать интерфейс telnet или curl.
Обычно это удобно для отладки конкретных джоб, чтобы другие не мешались.

Если же хочется непременно запустить локально с настоящим кварцем, чтобы все джобы по-настоящему запускались
в соответствии с расписанием, указанным в их триггерах, то в классах `MapiDatabaseSchedulerFactoryConfig` и
`MapiRamsSchedulerFactoryConfig` в строке внутри аннотации `@Profile` нужно указать другое значение.
Например, `!local`. Главное, потом это не закоммитить.

Примеры команд для RAMScheduler:
```shell
# краткоев руководство
echo "help" | nc localhost 33906
# список зарегистрированных TMS задач
echo "tms-list" | nc localhost 33906
# запуск задачи по имени джобы (можно получить с помощью "tms-list")
echo "tms-run executorName" | nc localhost 33906
```
