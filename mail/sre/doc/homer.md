### Что делает сервис
Проверяет авторизацию пользователя и направляет/редиректит в нужный компонент (liza/touch/lite)
или показывает стартовую страницу Почты до залогина с формой авторизации.

### Импакт на пользователей от отключения сервиса
Потенциально – невозможность войти в Почту из-за отключение редиректа в нужный компонент.

### Импакт остановки тачки/ДЦ
Нагрузка балансируется, импакта быть не должно.

### Особенности деплоя
В окружении каждый ДЦ выделен в отдельную компоненту.

### Критичные метрики
####5xx
Количество 5xx кодов ответа.

####4xx
Количество 4xx кодов ответа.

### Куда ходит
akita, meta, furita, captcha, setter, smslink, user split

