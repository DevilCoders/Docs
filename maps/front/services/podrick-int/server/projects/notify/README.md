# Уведомления для Qloud

## Email

Уведомляет членов ABC сервиса, привязанного к приложению, о выкладке окружения в Qloud. Также можно дополнительно добавлять получателей.

__Адрес__: `/notify/webhook/email/`

__Метод__: `POST`

__Параметры__:

* `query.users` — список ников, которым дополнительно отправится письмо. Например, `users=username1%2Cusername2`.
* `query['excluded-users']` — список ников, которым не надо отправлять письмо, даже если они есть в сервисе ABC. Например, `excluded-users=username1%2Cusername2`.
* `query['skip-abc']=1` — не отправляет уведомление пользователям из ABC сервиса, только из параметра `users`, по умолчанию `0`.
* `query['abc-role']` — список идентификаторов ролей ABC сервиса, разделенных запятой, которым надо отправить письмо, по умолчанию разработка, администрирование и дежурные.

**Важно**: запятые используются для разделения списка хуков. Поэтому если вы используете запятые в самом хуке, то не забывайте их писать в `%2C` виде.

### Заголовки письма

Для удобной фильтрации к письму добавляются кастомные заголовки:

* `X-Qloud-Deploy` — значение всегда `yes`.
* `X-Qloud-Deploy-Status` — текущий статус окружения.
* `X-Qloud-Deploy-Version` — текущая версия окружения.
* `X-Qloud-Deploy-Author` — автор деплоя.
* `X-Qloud-Project` — проект.
* `X-Qloud-Application` — приложение.
* `X-Qloud-Environment` — окружение.

## `.qtools.json`

Пример для использования в [qtools](https://github.yandex-team.ru/maps/qtools):

```json
{
    "qloud": {
        "testing": {
            "policies": {
                "deployHook": "https://podrick.c.maps.yandex-team.ru/notify/webhook/email/",
                "keepEsIndicesDays": 5,
                "shipAccessLog": true
            }
        }
    }
}
```
