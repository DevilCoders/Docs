## Выкатка
Выкатка производится путем генерации и заливки спецификации Ya.Deploy. Для генерации спеки необходимо собрать два sanbdox-ресурса: конфиг и само приложение. Если менялось только приложение (не ,было изменений внутри `tavern/tools/fs`), то достаточно:

    1) запушить ветку (с открытым PR)
    2) дождаться зеленого CI
    3) сгенерировать и залить спецификацию (см. ниже).

<details>
<summary>
Если менялся конфиг (tavern/tools/fs/…)
</summary>
Если менялись файлы внутри `tavern/tools/fs`, то:

    1) сделать `make mailfront-config` в корне проекта
    2) узнать id собранного ресурса – https://sandbox.yandex-team.ru/resources?type=MAILFRONT_CONFIG&limit=3&attrs=%7B%22component%22%3A%22tavern%22%7D
    3) поменять id ресурса в шаблоне `front-app.j2`
</details>

### Выкатка prestable ([tavern-prestable.mail.yandex.ru](http://tavern-prestable.mail.yandex.ru))
    1) Генерация спеки `make prestable`
    2) Деплой спеки `make put-prestable`

### Выкатка prod ([tavern.mail.yandex.ru](http://tavern.mail.yandex.ru))
    1) Генерация спеки `make prod`
    2) Деплой спеки `make put-prod`
    3) Апрув деплой тикета (ссылка выплюнет последняя команда)
