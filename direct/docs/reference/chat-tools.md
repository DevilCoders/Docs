# Чатовые инструменты

Какая работа с чатами есть в Директе

## direct-chat-bot-tools

Отдельные скрипты, которые отправляют сообщения в ТГ/Q непосредственно через API мессенджеров.

Репозиторий: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/direct-chat-bot-tools>

Запускаются из крона `ppcdev-scripts-cron` на `ppcdev`.

Лучше бы переделать на `direct-chat-bot.py --one-time-reply`

Собирается пакет `yandex-du-direct-chat-bot-tools`, его выкладывать на `ppcdev`-ы.


## direct-chat-bot.py

Основной скрипт, реализующий Директовых чат-ботов. 

Репозиторий: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/direct-chat-bot-universal/bin/direct-chat-bot.py>

Может работать с ТГ и Q. Может запускаться в режиме демона и слушать новые сообщения, может отправлять разовые сообщения (параметр `--one-time-reply`).

Запускается из кронов:  
- `yandex-du-ppcback-directadmin-cron` на `ppcback` (`--one-time-reply`)
- `yandex-du-ppcdev-scripts-cron` на `ppcdev` (`--one-time-reply`, демон)


## Табула / yamb_send 

Способ отправить сообщение в Q через http-ручку Табулы. 

Репозиторий: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/releaser/trunk/releaser/common/views.py> 


## Отдельный сервис отправки сообщений 

Способ отправить ТГ-сообщение через http-ручку.

Код в личном бранче у lena-san@, процесс запущен в `screen` на `ppcdev4`.

Используется в автосборке релизов.

Примеры:

```
curl 'http://ppcdev4.yandex.ru:5000/get_chat_info?bot=yd_herald&chat_id=-1001359667477'             
{"chat_info": {"id": -1001359667477, "title": "Title"}}

curl 'http://ppcdev4.yandex.ru:5000/set_title?bot=yd_herald&chat_id=-1001359667477&title=Title' 
{"ok": 1}

curl 'http://ppcdev4.yandex.ru:5000/send_message?bot=yd_herald&chat_id=-1001359667477&message=огого!'
{"ok": 1}

# сообщение без звука
curl 'http://ppcdev4.yandex.ru:5000/send_message?bot=yd_herald&chat_id=-1001359667477&message=огого!&quiet=1'
{"ok": 1}
```

