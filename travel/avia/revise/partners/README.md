Имена файлов соответствуют кодам партнёров.

Обязательная функция extractor в модуле должна выкидывать
yield'ом сообщения о ходе проверки.
Можно кидать ```ScreenShot(driver, <message>)```.
Последним элементом должен быть словарь c ключами
'price', 'currency'.


###### Размечаю так:
```
seiv@seiv.cloud.dev.rasp.yandex.net ~/work/standalone_ticket_daemon/ticket_daemon
$./manage.py run_path tools/query_mbo.py -k c213_c54_2016-01-12_None_economy_2_1_1_ru -v -p <partner_code>
```

Открываю url в браузере, подбираю xpath к элементу с ценой
