В *.properties нужно указать WmsTvmServiceId и WmsTvmSecret

WmsTvmServiceId можно найти тут: https://abc.yandex-team.ru/services/wms/resources/?show-resource=21874991 на вкладке Ресурсы, ресурс с типом "TVM приложение".
WmsTvmSecret задаётся через секретницу, значение там же в client_secret.
Для доступа нужна роль "TVM менеджер"
 
На сервере должен быть установлен пакет libticket-parser2-java 
