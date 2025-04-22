# telegram-client - клиент для работы с api Телеграма

### Описание
Клиент используется для отправки ответов на запросы пользователя в телеграм-бота Директа.
Бот: http://t.me/YandexDirectBot
Для работы с API телеграма клиенту необходим секретный токен.
Токен для работы в продакшене с API Телеграма храним в Секретнице:
https://yav.yandex-team.ru/secret/sec-01et2nxfxhztmzfba1z9x1pz8r

Реализовано два метода из API Телеграма:
* getMe - для проверки возможности делать запросы в API Телеграма (https://core.telegram.org/bots/api#getme)
* sendMessage - метод для отправки сообщений в чат (https://core.telegram.org/bots/api#sendmessage)

### Для тестирования
Можно использовать бота http://t.me/Direct_gukserg_test_bot
Токен для него лежит здесь:
https://yav.yandex-team.ru/secret/sec-01erykybfeh3neh4tpb5aqdm2y


