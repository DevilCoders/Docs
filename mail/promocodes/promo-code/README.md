#Локальный запуск:
## Сгенерим проект в IDE
    ya ide idea --directory-based --iml-in-project-root -lr ~/IdeaProjects/promocodes .
## Создадим базу данных
    create database promo;
    create user promo with encrypted password 'promo';
    grant all privileges on database promo to promo;
## Перекроем локально свойства в файле context-[hostname]-development.properties
    datasource.psql.url=jdbc:postgresql://localhost/promo
    datasource.psql.username=promo
    datasource.psql.password=promo

## Запускаем Run/Edit Configuration... 
    Main class: ru.yandex.mail.promocode.Application   

## Можно стрелять
    curl -d "@data.json" -H "Content-Type: application/json" -X POST http://<host>/api/promo/upload?tag=<tag>
data.json:
    [“<code1>”, “<code2>”, … , “<codeN>”]

    curl -X GET 'https://<host>/api/promo/assign?tag=<tag>&uid=<uid>&device_id=<device_id>