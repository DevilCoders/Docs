Описание
====
Утилита для выгрузки данных по утилизации GPU ABC сервисами

Данные складываются в [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/reserves/d_quota_requests)
и выводятся на [дашборд](https://datalens.yandex-team.ru/h0rz0sm0ad6a9-quotas-requests)


--------
Запуск
====
Автоматический
--
Утилита автоматически запускается каждый день в Nirvane.

Локально
----
Для запуска утилиты необходимо передать параметры:
* --token - токен Dispenser`a
* --campaigns - номера кампаний по сбору заявок через пробел
* --clouds - названия провайдеров через пробел

Пример (запуск из папки arcadia/infra/capacity_planning/utils/quota_requests):
```
ya make
./quota_requests --token <token> --campaigns 40 41 7 8 9 --clouds yp gencfg

```
Токен можно получить по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=fe21371385fa4ac8a24c2e9c318e0561)
