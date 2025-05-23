# Ключи и подписи

Для доступа к API нужен ключ - уникальный идентификатор, который позволяет связать запросы в API с соответствующим аккаунтом/тарифным планом. Для каждого ключа API настраивается [квота на нагрузку](quotas.md).

С ключом API связан секрет для подписывания запросов. Подпись запроса позволяет сервису убедиться, что запрос в API сгенерирован владельцем ключа.

## Как получить ключ API и секрет для подписывания { #new }

Призовите в ваш тикет [команду сервиса]({{ contacts_url }}) и напишите:
- какая ожидается [нагрузка](quotas.md),
- для какого abc-сервиса дать доступ к секретам (выдадим на scope:development, если отдельно не уточните роли).

Мы сделаем для вас ключи API (в формате uuid) и положим их в [секретницу](https://yav.yandex-team.ru/?tags=maps-staticapi-apikey).

Ключ API передается в запросе параметром `api_key`.

{% note tip %}

Рекомендуется для разных приложений и платформ использовать разные ключи API, чтобы превышение квоты в одном приложении не сломало сразу все.

{% endnote %}


## Как подписать запрос { #calc_signature }

Вместе с ключом API в [секретнице](https://yav.yandex-team.ru/?tags=maps-staticapi-apikey) лежит секрет для подписывания запросов - бинарные данные, закодированные [модифицированным Base64 для URL](https://en.wikipedia.org/wiki/Base64) алгоритмом.

Подпись передается в запросе параметром `signature`.

Алгоритм вычисления подписи: `base64url(HMAC_SHA256(signing_secret, URL))`
1. Сформировать URL запроса без параметра signature. Запрос должен включать параметр api_key с ключом API. Пример: `https://static-maps.yandex.ru/1.x/?l=map&ll=30.315868,59.939095&z=8&api_key=66e592f8-5b03-11eb-ae93-0242ac130002`
2. Убрать из URL запроса хост: `/1.x/?l=map&ll=30.315868,59.939095&z=8&api_key=66e592f8-5b03-11eb-ae93-0242ac130002`
3. Получить секрет для подписывания, связанный с ключом API. Раскодировать его из [Base64](https://en.wikipedia.org/wiki/Base64) строки в бинарные данные.
4. Вычислить из URL запроса код подписи алгоритмом [HMAC_SHA256](https://en.wikipedia.org/wiki/HMAC).
5. Закодировать код подписи [модифицированным Base64 для URL](https://en.wikipedia.org/wiki/Base64) алгоритмом.
6. Добавить к URL запроса параметр signature с полученной подписью. Пример: `https://static-maps.yandex.ru/1.x/?l=map&ll=30.315868,59.939095&z=8&api_key=66e592f8-5b03-11eb-ae93-0242ac130002&signature=LS6A6dzs09il9b2VsjAWr9YuRGzaeAYuw7CPD0M9KNo=`

{% cut "Вручную подписать запрос для отладки можно с помощью html-формы под катом (сохранить html локально и открыть в браузере)." %}

{% code '/maps/infra/apiteka/signature/url-signer.html' lang='html' %}

{% endcut %}


## Как разрешить неподписанные запросы { #allow_unsigned }

{% note alert %}

Мы не рекомендуем отключать проверку подписей, особенно на вебе. Ключ API открыто передается в параметрах URL, его легко узнать и использовать чужую квоту в сторонних сервисах если запросы не защищены подписью.

{% endnote %}

Вы можете попросить [команду сервиса]({{ contacts_url }}) отключить проверку подписи (разрешить неподписанные запросы) для любого из ваших ключей API, или наоборот запретить обрабатывать неподписанные запросы если для ключа API они были разрешены ранее.

Настройка влияет только на запросы с отсутствующей подписью. Запросы с правильной подписью обрабатываются всегда, на неправильно подписанные запросы всегда возвращается код ошибки 403 Forbidden.

{% note tip %}

Используйте разные ключи API для приложений, которые не могут использовать подписи и для тех, которые подписывают запросы.

{% endnote %}


## Старые ключи API { #legacy }

Если вы используете старые ключи API вида `ADuxd18BAAAAopuNLAIAFWiYfzaA8aRJFEabpjprggGINu4AAAAAAAAAAABQ0t29spPxz3IDyODhmiK_fXX0xg==` без подписей и передаете их параметром `key`, напишите [нам]({{ contacts_url }}), мы сделаем вам новый ключ.

Для старых ключей недоступны все новые фичи в API:
- индивидуальная квота
- темная тема
- кастомизация карты
- OSM


## Личный кабинет (в планах)

Мы планируем сделать личный кабинет, в котором можно будет самостоятельно создавать новые ключи API, менять их настройки или блокировать скомпрометированные ключи API.
