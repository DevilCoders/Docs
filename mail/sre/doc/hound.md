### Что делает сервис
Сервис над почтовой метабазой для выдачи списков папок, меток, табов и списков писем с разными условиями.

### Импакт на пользователей от отключения сервиса
Полная незагрузка Почты у пользователя, ошибка в интерфейсе пользователя.

### Импакт остановки тачки/ДЦ
Балансер перераспределяет нагрузку между другими тачками/дц, внешнего импакта наблюдаться не должно.

### Особенности деплоя
Могут наблюдаться рост таймингов и ошибок, которые покрываются ретраями.

### Критичные метрики

####hound_nginx_5xx
Количество 5xx кодов ответа.

####hound_nginx_4xx
Количество 4xx кодов ответа.

### Куда ходит

#### mdb (macs_pg)
Получение списка папок, писем, меток, табов.

#### sharpei (http_client)
Получение шарда mdb для пользователя.

#### mds (http_client)
Получения частей тел писем.

