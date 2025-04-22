# Сверка ежемесячных отчётов по оказанным услугам

## Общее описание

Партнёр или наш сотрудник скидывает письмо с прикреплённым отчётом на определённый почтовый адрес.
Далее регулярный [Hitman процесс](https://hitman.yandex-team.ru/projects/travel-cpa-prod/travel-cpa-prod-reconciliation/)
периодически обрабатывает эти письма:
- считывает новые письма из специальных партнёрских папок во Входящих сообщениях
- выполняем сверку отчёта с данными из CPA платформы
- создаёт тикет в Трекере, указывая результаты сверки и прикладывая файлы исходного и результирующего отчёта
- отмечает письмо как обработанное, перемещая его в отдельную специальную папку

Примеры адресов и отчётов можно найти в тикете на сверки - [YATRAVELBD-160](https://st.yandex-team.ru/YATRAVELBD-160)

## Локальная отладка

При разработке нового отчёта или отладке старого удобнее обрабатывать его без подключения к удалённому почтовому серверу
и без заведения задач в Трекере. Для этого можно воспользоваться опцией `--debug-mode`:

```
# from travel/cpa/data_check/reconciliation
ya make
./reconciliation --debug-mode --vault-token ${VAULT_TOKEN} --yt-token sec-01d1x4rf3p808k64h608xh89qq \
    --st-token not_used --imap-token not_used
```

`VAULT_TOKEN` можно взять или [свой](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982),
или от [тестового робота](https://yav.yandex-team.ru/secret/sec-01daxhj3d3824zq53vc06c11e7/explore/version/ver-01daxhj3dhwexh29fbbcm7k6fz).

## Полная локальная отладка

Для полноценной проверки отчётов со своей машины можно отправить письмо на `robot-travel-testing@yandex-team.ru`.
Сперва убедиться, что оно перекладывается автоматическими правилами подписки в нужно папку по входящих. Далее
запустить инструмент с полным набором аргументов и без `--debug-mode`:

```
./reconciliation --login robot-travel-testing@yandex-team.ru --imap-token sec-01d83kawsae4gwh115nyn1sr5x.imap-token \
    --vault-token ${VAULT_TOKEN} --yt-token sec-01d1x4rf3p808k64h608xh89qq \
    --st-token sec-01d83kawsae4gwh115nyn1sr5x.startrek-oauth-key \
    --related-issue <TEST_TICKET> --assignee <TEST_LOGIN> --partner <PARTNER_NAME>
```
