# Yandex.Pay

## About

wiki: https://wiki.yandex-team.ru/yandexpay/
abc: https://abc.yandex-team.ru/services/yandexpay

Yandex.Pay - сервис быстрой оплаты онлайн и оффлайн без ввода карточных данных.
Использует технологию токенизации карт.

## Список проектов
* https://a.yandex-team.ru/arc/trunk/arcadia/billing/yandex_pay - бэкенд карточных данных. Занимается токенизацией карточных данных из Trust. Обслуживает запросы платежной формы pay, мобильной pay sdk, оффлайн pay sdk.
* https://a.yandex-team.ru/arc/trunk/arcadia/billing/yandex_pay_plus - бэкенд истории платежей Yandex.Pay. Содержит таймлайн жизненного цикла заказа, оплаченного через Yandex.Pay - платежные шлюзы отстукивают нам статусы. Так же содержит логику начисления кэшбэка в рамках программы лояльности.
* https://a.yandex-team.ru/arc/trunk/arcadia/billing/yandex_pay_admin - бэкенд личного кабинета Yandex.Pay (Console). Нужен мерчантам и шлюзам для настройки интеграции с Yandex.Pay.
* https://a.yandex-team.ru/arc/trunk/arcadia/pay/frontend/services/console - фронтенд личного кабинета мерчанта/psp.
* https://github.yandex-team.ru/yandex-pay/duckgo - небольшой бэкенд, отвечающий за токенизацию и за формирование YandexPayToken. Сертифицирован по PCI DSS, размещается в PCI DSS окружении Trust.
* https://github.yandex-team.ru/trust/yandex-pay - платежная форма Yandex.Pay. Имеет два режима: платежная форма (выбрал карту и оплатил) и 1-Click-Checkout (с предоставлением мерчанту контактных данных и другого контекста). Сертифицирован по PCI DSS.
* https://github.yandex-team.ru/trust/ci-frontend - инструментарий для выкатки релизов платежной формы в соответствии с требованиями PCI DSS.
* https://a.yandex-team.ru/arc/trunk/arcadia/mobile/yandex-pay/nfc - оффлайн sdk для платежей в POS терминалах через технологию nfc
* https://a.yandex-team.ru/arc/trunk/arcadia/mobile/yandex-pay/ios - мобильная sdk для онлайн платежей в мобильных приложениях iOS
* https://a.yandex-team.ru/arc/trunk/arcadia/mobile/yandex-pay/android - мобильная sdk для онлайн платежей в мобильных приложениях Android
