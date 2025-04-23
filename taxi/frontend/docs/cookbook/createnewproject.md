# Как создать новый фронтенд сервис

Новые сервисы заводятся в [монорепе такси](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/frontend/), которая имеет общие тулы для сборки и релизов сервиса.
Процесс заведение нового сервиса описан [здесь](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/?from=%252Ftaxi%252Fweb%252Fhiring-projects%252Frtc%252F#procedurazaezda).

Если кратко, то флоу выглядит так:
1. Создать инстансы в RTC
2. Пройти архревью RFC сервиса
3. Настроить сборку вашего проекта
4. Пройти ревью от ИБ
5. Релиз и открытие во вне

{% note warning %}

Всегда помни и соблюдай [рекомендации](https://wiki.yandex-team.ru/security/for/web-developers/) от ИБ при разработке сервиса. Персональные данные и токены не должны оседать в логах, а так же фигурировать в исходниках проекта

{% endnote %}