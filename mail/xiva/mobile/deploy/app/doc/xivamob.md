### Что делает сервис
Сервис реализует отправку пушей в мобильные облака - APNs(iOS), FCM(android), HMS(Huawei), WNS и MPNS (Microsoft) или в браузеры по WebPush протоколу.

### Импакт на пользователей от отключения сервиса
Пользователи не будут получать пуши для приложений на мобильных устройствах и в браузеры по WebPush протоколу.

### Импакт остановки тачки/ДЦ
Балансер должен перенаправить нагрузку на другие тачки/ДЦ, нагрузка на них возрастет пропорционально.

### Особенности деплоя
Катим canary, смотрим на графики. При отсутствии проблем катим основной компонент.

### Критичные метрики
#### xivamob_5xx

### Куда ходит
#### xivaconf (http_client)
Чтение из xivaconf списка зарегистрированных приложений (раз в n минут).
#### Мобильные облака (http_client)
Отправка пушей в мобильные облака - APNs (используется http2), FCM, HMS, MPNS, WNS.
#### Web Push (http_client)
Отправка пушей в браузеры.
