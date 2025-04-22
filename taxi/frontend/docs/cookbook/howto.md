# how to такси фронтенд

Здесь собраны основные рецепты и готовые решения для разработки фронтенд проекта. Как правило, это покрывает 90% нужд проекта.

## Сервисы

### TVM
[TVM](https://wiki.yandex-team.ru/passport/tvm2) необходим для подписи и проверки подписи back to back запросов. Другими словами, это способ проверить должен ли сервис B доверять запросу от сервиса A и идентифицировать этот сервис.

**Как подключить к сервису**:

`1.` Идём во вкладку "Ресурсы" вашего сервиса в ABC (Сылку можно найти на страничке сервиса в админке [так](https://tariff-editor.taxi.yandex-team.ru/services/)). Если ресурс "Паспорт" еще не заведён, то запрашиваем его. Если ресурс есть - вам понадобится его ID и client_secret (она разные для testing и production).

{% cut "screen" %}

![](https://jing.yandex-team.ru/files/twin/tvm_1.png)

{% endcut %}

`2.` Идём на вкладку TVM правила в [админке вашего сервиса](https://tariff-editor.taxi.yandex-team.ru/services/). Добавляем необходимые правила (**Входящие** - для прилетающих в ваш сервис запросов, но такое почти не используется в фронтенд проектах и **Исходящие** для подписи ваших запросов к другим сервисам). Не забываем прописывать правила для всех окружений.

_Если необходимого сервиса нет в списке "TVM имена приёмников", то нужно расширить конфиг [TVM_SERVICES](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/TVM_SERVICES?name=TVM)_

`3.` Учим сервис ходить в tvm демона

#### Локально (или на dev машинке):
`1.` Необходимо положить конфиг tvm в хомяка.

{% cut "Пример конфига" %}

```js
{
  "clients": {
    "taxi-frontend-yandex": { // название сервиса
      "secret": "$CLIENT_SECRET", // секрет полученный на шаге 1
      "self_tvm_id": 2023370, // ID полученный на шаге 1
      "dsts": { // Название и ID сервисов заданных в админке на шаге 2
        "passport": {
          "dst_id": 224
        }
      }
    }
  }
}
```

{% endcut %}

_Сам конфиг нельзя сохранять в репозитории проекта, т.к. он содержит секретный ключ. Рекомендуем положить конфиг к [секретницу](https://yav.yandex-team.ru/) и дать доступ команде до него._

`2.` Установить tvm-tool демона и запускать его при старте сервиса. Подробно описано [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/express-tvm#podklyuchenie-lokalno)

#### В облаке (RTC)

`1.` Необходимо прописать переменные окружения вашего сервиса в админке во вкладке "Секреты". Указать значения
```
    "use_local_tvmtool": true,
    "app_env": "{{ FREEFORM_ENVIRONMENT }}",
    "local_tvmtool_use_bb_by_env": true
```

`2.` Примеры использования tvm в живых проектах:
- С express: [tvmtool](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/frontend/services/taxifrontend/projects/yandex/server/index.js?rev=r9303241#L27), [конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/frontend/services/taxifrontend/projects/common/server/utils/tvm-secret.js?rev=r9303241), [middleware](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/frontend/services/taxifrontend/projects/common/server/middleware/tvm.js?rev=r9303241), [подпись запроса](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/frontend/services/taxifrontend/projects/common/server/api/experiments.js?rev=r9303241#L11)
- С nest: [tvmtool](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/frontend/services/hiring-mass-frontend/src/tvmtool/index.ts?rev=r9303241), [config](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/frontend/services/hiring-mass-frontend/src/server/app.module.ts?rev=r9303241#L41), [package](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/nest-infra/src/tvm/README.md)

### Blackbox
[UserTicket](https://docs.yandex-team.ru/blackbox/) (черный ящик или ЧЯ) необходим для авторизации пользователя на сервисе (портальная авторизация). За счет обмена пользовательских кук или токена на данные о пользователе. Так же blackbox позволяет обменять куку пользователя на коротко-живущий ((https://wiki.yandex-team.ru/passport/tvm2/user-ticket/) для дальнейшей передачи в бекенд

**Как подключить к сервису**:
Запросы в API blackbox делаются с nodejs (back to back). Запросы необходимо подписывать TVM тикетом. Для получения доступа к API из нового сервиса, необходимо [проковырять дырки и запросить гранты](https://docs.yandex-team.ru/blackbox/concepts/getting-access)
Важно правильно выбрать [окружение](https://docs.yandex-team.ru/blackbox/concepts/location)

Окружение сервиса | host blackbox | TVM id | passport host
:--- | :--- | ---: | ---:
development/testing/unstable | blackbox-test.yandex.net | 224 | https://pasport-test.yandex.ru
production | blackbox.yandex.net | 222 | https://passport.yandex.ru
yandex-team (any) | blackbox.yandex-team.ru | 223 | https://passport.yandex-team.ru

Чтобы прилетал верный tvm тикет, нужно в админке вашего сервиса во вкладку TVM правил, указать необходимые tvm id

Готовая библиотека для общения с blackbox:
- [для expressjs](https://a.yandex-team.ru/svn/trunk/arcadia/frontend/packages/express-blackbox)
- [для nestjs](https://a.yandex-team.ru/svn/trunk/arcadia/frontend/packages/nest-infra/src/blackbox/README.md)

Примеры использования на проектах:
- [taxifrontend express](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/taxifrontend/projects/common/server/middleware/blackbox.js)
- [mass-frontend nest](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/hiring-mass-frontend/src/server/app.module.ts)
- [получение user-ticket](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/market-bo/server/src/common/passport/blackboxMiddleware.ts?rev=r9614265#L78)

**Важно** убедиться, что в ЧЯ вы передаёте именно ip пользователя, а не ДЦ

### Geobase
Сервис необходим, если у вас стоит задача определять положение пользователя по ip адресу или куке gid на стороне сервера.
Используется [http-geobase](https://a.yandex-team.ru/svn/trunk/arcadia/frontend/packages/express-http-geobase). Сама база доступна по урлу [https://geoadmin.yandex-team.ru](https://geoadmin.yandex-team.ru)

Пример в сервисе: [taxifrontend](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/taxifrontend/projects/common/server/utils/geobaseHelper.js)

**Важно** убедиться, что в геобазу вы передаёте именно ip пользователя, а не ДЦ

### UATraits
Сервис необходим, если у вас стоит задача определить устройство пользователя (платформа/мобилка/модель)
Используется [http-uatraits](https://a.yandex-team.ru/svn/trunk/arcadia/frontend/packages/express-http-uatraits)

### Tirole
[Tirole](https://wiki.yandex-team.ru/passport/tvm2/tirole) позволяет получить список ролей сервиса для последующей проверки доступов.

**Как подключить к сервису**:
Интеграция делается через [tvmtool](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/), а именно ручки /check и /roles

Пример в проекте:
[market-bo](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/market-bo/server/src/common/acl?rev=r9614265) _(текущее решение реализовано поверх питон скрипта, т.к. подержки в tvmtool еще не было)_

### Experiments 3.0
Сервис [экспериментов](https://wiki.yandex-team.ru/taxi/backend/architecture/experiments3/Manual/) позволяет проводить A/B тестирование и плавно раскатывать новую функциональность по пользователям.

UI для создания экспериментов: https://tariff-editor.taxi.yandex-team.ru/experiments3/

**Как подключить к сервису**:
`1.` Настраиваем tvm правила вашего [сервиса](https://tariff-editor.taxi.yandex-team.ru/services/), добавляя туда сервис экспериментов.

{% cut "Скрин" %}

![](https://jing.yandex-team.ru/files/twin/experimants.png)

{% endcut %}

#### Настраиваем серверную часть вашего приложения

Учим ваше приложение получать эксперименты из API [yaml](https://a.yandex-team.ru/arcadia/taxi/backend-cpp/experiments3/docs/yaml/experiments3.yaml?rev=r9324981#L6)

Окружение | Хост
:--- | :---
production | http://experiments3.taxi.yandex.net/v1/experiments
testing | http://experiments3.taxi.tst.yandex.net/v1/experiments

Важно правильно составить тело запроса (по мимо подписи tvm), а именно указать **консьюмера** и **кварги** вашего сервиса.

- **Консьюмер** - это по факту имя вашего сервиса, именно на консьюмера заводятся эксперименты.
- **Кварги** - это параметры по которым будут матчиться эксперименты, например id юзера, или язык/страна пользователя и тп. Каждый сервис волен указать произвольный набор кваргов, но желательно придерживаться единообразия в именовании.

Обязательными кваргами являются **application** и **version**, при этом version должен строго соответствовать semver

{% cut "Пример тела запроса для сервиса taxi.yandex.ru" %}

```json
{
    "consumer": "taxi-frontend-yandex",
    "args": [
        {
            "name": "application",
            "type": "application",
            "value": "taxi-frontend"
        },
        {
            "name": "version",
            "type": "application_version",
            "value": cfg.app.version
        },
        {
            "name": "language",
            "type": "string",
            "value": req.langdetect.id
        },
        {
            "name": "tld",
            "type": "string",
            "value": req.tld
        },
        {
            "name": "country",
            "type": "string",
            "value": country
        },
        {
            "name": "os",
            "type": "string",
            "value": req.ua.os
        },
        {
            "name": "yandex_uid",
            "type": "string",
            "value": xYandexUid
        },
        {
            "name": "yandex_login",
            "type": "string",
            "value": login
        }
    ]
}
```

{% endcut %}

Пример в коде проектов:
- [express](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/taxifrontend/projects/common/server/api/experiments.js)
- [nest](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/hiring-mass-frontend/src/server/core/experiments/experiments.service.ts)

`2.` Заводим первый эксперимент в ui

{% cut "Подробней" %}

1. Идём на страницу [экспериментов](https://tariff-editor.taxi.tst.yandex-team.ru/experiments3)
2. Заводим нового потребителя (consumer). Он должен быть равен тому, что вы указали в запросе
3. Создаём эксперимент указывая вашего консьюмера и необходимые вам кваргки (для теста можно оставить только условие "всегда включен"

Подробней про ui экспериментов есть [видеозапись](https://s386vla.storage.yandex.net/rvideo-nda/U2FsdGVkX19MifNFLaMSBcxRp4X32QR6PaL6pGb2-_no8wMG48WJ9X74YWvzgjnINT48OkAn4Q7p3LD3b-9aDmds4o58r06B13NiSBVhCz8?ts=0005e3c1d739311e&sign=de997de230796e2d653d6541ab88912372b4b71b47ab37501531dc05e9fe91a5) встречи

{% endcut %}

### Конфиги 3.0
Сервис [конфигов](https://wiki.yandex-team.ru/taxi/backend/architecture/configs/manual) позволяет проводить фичатогл в сервисе либо динамически конфигурировать часть сервиса

**Как подключить к сервису**:

Конфиги 3.0 отличаются от экспериментов отсутствием срока действия, в остальном очень похожи.

API [yaml](https://a.yandex-team.ru/arcadia/taxi/backend-cpp/experiments3/docs/yaml/experiments3.yaml?rev=r9324981#L20)

Окружение | host
:--- | :---
production | http://experiments3.taxi.yandex.net/v1/configs
testing | http://experiments3.taxi.tst.yandex.net/v1/configs

{% cut "Пример запроса" %}

```bash
curl -X POST \
  http://experiments3.taxi.tst.yandex.net/v1/configs \
  -H 'Content-Type: application/json' \
  -d '{
    "config_name": "default_config",
    "consumer": "taxi-frontend",
    "args": [
        {
            "name": "application",
            "type": "application",
            "value": "android"
        },
        {
            "name": "version",
            "type": "application_version",
            "value": "3.85.0"
        }
    ]
}'
```

{% endcut %}

## Локализация (i18n)

Сами ключи хранятся в системе [Танкер](https://wiki.yandex-team.ru/l10n/tanker/). В танкере есть проекты, в проектах кейсеты, в кейсетах список ключей (ну и есть еще бранчи).
С танкером работают переводчики, выгружая ключа и заливая переводы.

Танкер имеет [API](https://wiki.yandex-team.ru/l10n/tanker/#api), через которое можно подтягивать переводы в проект и загружать новые ключи.

{% note tip %}

При создании нового сервиса, важно сразу подумать о локализации, т.к. внедрять её в уже большой готовый проект - дорого.

{% endnote %}

**Возможные подходы к работе с локализацией**:
- Выкачивать файлы с переводами в момент сборки сервиса и хранить их вместе с исходным кодом.

Из плюсов: типизация, возможность синхронизировать код с переводами

Из минусов: требует релиза новой версии приложения для обновления переводов

- Подтягивать переводы динамически через BFF часть

**Инструменты**:

1. [tanker-kit](https://a.yandex-team.ru/svn/trunk/arcadia/frontend/packages/tanker-kit) . Пример использования [в проекте](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/txf-family-frontend/.tanker)
2. [taxi-localization](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/packages/taxi-localization) - Позволяет распарсить русские тексты в проекте и заменить на вызов i18n

## Метрика

Большинство продуктовых сервисов нуждаются в продуктовых метриках, например - сколько раз нажали на кнопку А, и сколько раз заполнили поле Б. Для этого обычно используется [Яндекс.Метрика](https://yandex.ru/support/metrica/)

- [wiki](https://wiki.yandex-team.ru/jandexmetrika/)
- [ui](https://metrika.yandex.ru)

Правила создания счетчика для сервиса яндекса [тут](https://wiki.yandex-team.ru/jandexmetrika/counter-transfer/)

Вставить сам счетчик можно как указано в документации через скрипт, но удобней использовать пакет [react-yandex-metrika](https://www.npmjs.com/package/react-yandex-metrika)

## Яндекс.Формы

Для простых пользовательских форм желательно использовать сервис [Конструктор форм](https://wiki.yandex-team.ru/forms/), вставляя их через iframe.

Iframe кидаем через PostMessage события:
1. `iframe-height` - изменение величины контента
2. `iframe-offset` - отступ до первой ошибки при валидации (что бы проскролить страницу)

## Статичные лендинг страницы

Всё что может быть сделано на конструкторе лендингов силами менеджеров, нужно делать на [конструкторе лендингов](https://wiki.yandex-team.ru/lp-constructor/).

Так же есть возможность показывать страницы лендинга на своём домене, через nginx проксирование. Для этого нужно:
1. Завести папку с именем вашего домена в конструкторе лендингов. Пример тикета
2. Настроить nginx на вашей стороне

{% cut "Пример nginx конфига для go.yandex" %}

```
upstream lpc {
    # дублируем, чтобы не кешировалась ошибка
    server lpc-internal.yandex.net max_fails=0;
    server lpc-internal.yandex.net max_fails=0;
    keepalive 8;
}

server {
    server_name go.yandex;
    
    set $lp_constructor_host go.yandex;

    location ~ ^/(lp|doc|promo|signup)/ {
        proxy_set_header Host $lp_constructor_host;
        proxy_set_header X-Remote-Ip $http_x_real_ip;
        proxy_set_header X-Forwarded-For $http_x_real_ip;
        proxy_set_header X-Forwarded-For-Y $http_x_forwarded_for_y;
        proxy_intercept_errors off;
        proxy_buffer_size 8k;
        proxy_pass http://lpc/$request_uri;
    }
    
    # конструктор может делать запросы в данный урл, например за капчей
    location /promo/components/ {
        proxy_set_header Host $lp_constructor_host;
        proxy_set_header X-Remote-Ip $http_x_real_ip;
        proxy_set_header X-Forwarded-For $http_x_real_ip;
        proxy_set_header X-Forwarded-For-Y $http_x_forwarded_for_y;
        proxy_intercept_errors off;
        proxy_buffer_size 8k;
        proxy_pass http://lpc/promo/components/;
    }
}
```

{% endcut %}
