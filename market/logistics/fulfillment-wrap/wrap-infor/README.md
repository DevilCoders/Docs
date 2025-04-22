## Компонент Wrap Infor (Прослойка между FFSM и WMS Infor)


#### Как запускать: 
1. Сконфигурировать application-local.properties (см. application-local.properties.dist)
2. Сконфигурировать wrap-secrets.properties (см. wrap-secrets.properties.dist)
3. Создать локальный конфиг logback из шаблона [logback.xml.dist](src/main/conf/local/logback.xml.dist)  
4. Запускать через runLocal/run таску в gradle со следующими VM аргументами:
-Dlog.dir=<log_dir> -Denvironment=local


#### Как сделать инкремент склада:
1. Добавить в секретницу конфиг для нового склада. Пример, где `wh1` - это какое-то имя для описания склада:
```
fulfilment.wrap.infor.warehouse.wh1.token=XXXXXsome_tokenXXXXX
fulfilment.wrap.infor.warehouse.wh1.id=yandex_id
fulfilment.wrap.infor.warehouse.wh1.partnerId=partner_id
fulfilment.wrap.infor.warehouse.wh1.datasource.url=jdbc:sqlserver://sql-rst.mast.yandex-team.ru;database=WRAP_INFOR
fulfilment.wrap.infor.warehouse.wh1.datasource.username=some_username
fulfilment.wrap.infor.warehouse.wh1.datasource.password=some_password

fulfilment.wrap.infor.warehouse.wh1.client.enterpriseKey=enterpriseKey
fulfilment.wrap.infor.warehouse.wh1.client.warehouseKey=warehouseKey
fulfilment.wrap.infor.warehouse.wh1.client.username=username
fulfilment.wrap.infor.warehouse.wh1.client.password=password
fulfilment.wrap.infor.warehouse.wh1.client.url=http://some_url/scprd/wmwebservice_rest
```

2. Добавить новую quartz джобу по аналогии с `RovQuartzJobsConfiguration`, где:
   * указать в конструкторе путь к токену от `wh1` из п.1: `@Value("${fulfilment.wrap.infor.warehouse.wh1.token}")`
   * добавить префикс склада ко всем методам в конфигурации:
   ```java
       public Executor wh1PushStocksUsingDepositEvents(...)
       ...
       public Executor wh1PushStocksUsingWithdrawalEvents(...)
       ...
       public Executor wh1PushStocksUsingHoldEvents(...)
       ...
   ```
   Джобы для выгрузок в YT должны быть разнесены по времени, так как лочат одну и ту же таблицу:
   wh1ReceiptToYtUpload и wh2ReceiptToYtUpload не должны запуститься в одно время так же как и
   wh1ReceiptDetailToYtUpload и wh2ReceiptDetailToYtUpload.
