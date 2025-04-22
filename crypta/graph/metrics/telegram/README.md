Telegram bot BB8
========================

Рассылает ежедневный диф по метрикам склейки. 

Username в tg: _crypta_matching_bot_

Запущен в [https://sandbox.yandex-team.ru/scheduler/9961]

### Локальный запуск

Можно локально запустить бинарь и отправить себе в телеграмм сообщение. 
Для этого надо создать/узнать свой чат id с ботом: нужно добавить себе 
в контакты бота и написать ему что нибудь, а потом посмотреть по ссылке
в апи: https://api.telegram.org/bot<TOKEN>/getUpdates

```bash
$ ENV_TYPE=production TELEGRAM_TOKEN=<TOKEN> CHAT_IDS=<CHAT_ID> ./crypta/graph/metrics/telegram/telegram
```
