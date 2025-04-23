# Calendar Mailhook Processor

Это основная часть консьюмера по процессингу логов аттачей для создания встреч.

Оригинальная задача: [MPROTO-2760](https://st.yandex-team.ru/MPROTO-2760)

## Принцип работы

Получив очередную строку лога, мы узнаем

- что за пользователь в ББ (и является ли он рассылкой)
- в какой бд он находится (через шарпей)
- в бд достаем сдвиги в сторадже для календарного аттача
- узнаем кто адресат письма (в случае корповой рассылки идем в ml)
- сабмитим всю инфу + аттач из стораджа в календарь

## Связи с другими репо

- Прод конфиг: https://github.yandex-team.ru/mail/salt/tree/master/salt/components/logconsumer/conf
- Работа с ББ: https://github.yandex-team.ru/common-python/python-blackboxer
- Запуск консьюмера: https://github.yandex-team.ru/mail/logbroker-client-common

## Релизы

- Создать GH релиз
- Стриггерить появившийся тег в https://common.jenkins.mail.yandex.net/job/mail/job/calendar-attach-processor/view/tags/
    (или на том J который обслуживает Pipeline)

## Больше информации

https://wiki.yandex-team.ru/mail/logconsumers/

### Запуск тестов локально

Т.к. требуются твм библиотеки, на маке их достать сложно. Поэтому тесты проще запустить в
предподготовленном докере.

```
docker build -t pydev .
docker run -it --rm -v `pwd`:/code/ pydev pytest --cov=calendar_attach_processor
```
