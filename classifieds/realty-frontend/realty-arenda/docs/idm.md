# Доступ в админку

## Тестинг

1. Нужен пользователь в [тестовом паспорте](https://passport-test.yandex.ru/registration), который станет менеджером
2. В [бункере](https://bunker.yandex-team.ru/realty-www/arenda/test-managers?view=raw) нужно прописать соответсвие пользователя из тестового паспорта, пользователю из [тестового стаффа](https://staff.test.yandex-team.ru), чьи роли ему необходимо получить:
    ```
    {
        ...,
        "user123": "staffuser"
    }
    ```
3. Запрашиваем в [тестовом IDM](https://idm.test.yandex-team.ru/system/vsif/roles#rf=1,rf-role=xWOBWWDZ#vsif/EXTERNAL/ARENDA(fields:();params:()),f-status=all,sort-by=-updated,rf-expanded=xWOBWWDZ) нужные роли

*Данные из бункера и IDM прорастают в течении получаса*

## Прод

1. На [стаффе](https://staff.yandex-team.ru) нужно привязать паспортный аккаунт под которым будет происходить работа в админке
2. Запрашиваем в [продовом IDM](https://idm.yandex-team.ru/system/vsif/roles#rf=1,rf-role=fr3KpxsM#vsif/EXTERNAL/ARENDA(fields:();params:()),f-status=all,sort-by=-updated,rf-expanded=fr3KpxsM) нужные роли

*Данные из IDM прорастают в течении получаса*
