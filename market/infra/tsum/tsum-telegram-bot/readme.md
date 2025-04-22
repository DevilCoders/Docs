# Локальный запуск
1. Создать для себя собственного телеграм бота для целей отладки (можно в принципе использовать разработческого бота `@DevelopmentTSUMYandexBot`, но в таком случае есть риск конкуренции с другими бэкендами за этого бота, у кого-то что-то работать не будет, поэтому лучше создать своего). Процесс создания описан [тут](https://core.telegram.org/bots#3-how-do-i-create-a-bot). Нужно будет запомнить токен для HTTP API и username.
2. Создать файл `src/main/properties.d/local/99_local-overrides.properties`, не добавлять его в arc в диалоге после создания, позже он не будет отображаться в изменениях благодаря `../.arcignore`.
3. С использованием [тестовых](https://yav.yandex-team.ru/secret/sec-01d4mwzv17f5a7ba3y3sgcm4r4/explore/version/head) и [продовых](https://yav.yandex-team.ru/secret/sec-01d2104q8dmkydf0q6ny8cytm6/explore/version/head) секретов ЦУМа заполнить созданный файл пропертями:
```
tsum.telegram-bot.pg.jdbc.url=<взять из секретов тестинга>
tsum.telegram-bot.pg.jdbc.username=<взять из секретов тестинга>
tsum.telegram-bot.pg.jdbc.password=<взять из секретов тестинга>
tsum.telegram-bot.token=<взять токен от собственного бота, созданного ранее>

tsum.staff.auth-token=<взять из секретов прода>

tsum.duty.csadmin.incident.calendar_layer_id=41671
tsum.duty.csadmin.incident.duty-group-phone=7880

tsum.tvm.id=2009899
tsum.tvm.secret=<взять из секретов тестинга>
```
4. Собрать библиотеку `libticket_parser2_java.so` согласно [инструкции](https://wiki.yandex-team.ru/passport/tvm2/library/) (важно в точности следовать инструкции, выполняя `ya make` с необходимыми ключами именно из корня Аркадии, иначе файл `libticket_parser2_java.so` может так и не появиться. Если у полученного файла не будет флага на исполнение, его надо будет добавить с помощью команды `chmod a+x bin/libticket_parser2_java.so`).
5. Создать run-configuration для класса `TsumTelegramBotMain`. В run-configuration надо указать флаги для виртуальной машины `-Djava.library.path=/home/<имя пользователя>/arc/arcadia/bin -Dconfigs.path=/home/<имя пользователя>/arc/arcadia/market/infra/tsum/tsum-telegram-bot/src/main/properties.d` (путь указан в предположении, что аркадия примонтирована в домашний каталог в папку `~/arc/arcadia`)
6. После этого можно запускать созданную run-configuration, добавлять своего бота в чаты, писать ему в личку -- всё должно работать.
