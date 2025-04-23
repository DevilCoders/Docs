# bb_requester

## Зачем?
Утилита для ручных походов в поведенческий.
От походов с помощью `curl` она отличается следующим:
+ поддерживает tvm.
+ экранирует json с параметрами экспериментов.
+ адекватные параметры по умолчанию:
    + форматированный вывод
    + новый proto формат
    + bigb-fast в качестве сервера
+ некоторые дополнительные фичи, см. --help

## Использование
+ если нужно просто посмотреть на пользователя по куке, то:
    + `./bb_requester --uid 01603581507615744`
    + [(вывод)](https://paste.yandex-team.ru/690003/html)
+ если нужно просто посмотреть на пользователя из определенной машины:
    + `./bb_requester --host man1-0581-man-bigb-eagle-1-25245.gencfg-c.yandex.net:79 --uid 123123871550535168`
    + [(вывод)](https://paste.yandex-team.ru/690017/html)
+ если нужно просто посмотреть на пользователя из определенной машины на тестинге:
    + `./bb_requester --host man1-3729-man-bigb-eagle-dev-10-28295.gencfg-c.yandex.net:79 --test --uid 123123871550535168`
    + [(вывод)](https://paste.yandex-team.ru/690030/html)
+ если нужно передать параметры экспериментов:
    + `./bb_requester --exp-json '{"EagleSettings":{"MaxCommonQueries":10}}'  --uid 0`
+ любителям curl можно просто указать часть path после `/bigb?`:
    + `./bb_requester --curl "bigb-uid=123&client=yabs&format=protobuf"`
    + `./bb_requester "bigb-uid=123&client=yabs&format=protobuf"`
    + `./bb_requester "bigb-uid=123" "client=yabs" "format=protobuf"`

## Доступы
Если вы не из bigb, но хотите ходить от имени клиента своего сервиса [(см. таблицу)](https://wiki.yandex-team.ru/bigb/%D0%BF%D0%BE%D1%82%D1%80%D0%B5%D0%B1%D0%B8%D1%82%D0%B5%D0%BB%D0%B8-bigb/)
+ Идем в секретницу https://yav.yandex-team.ru/
+ Создаем Новый секрет с парами
    + Ключ - `tvm_ticket_id`, значение - id своего tvm-приложения (вы нам его сообщали при создании клиента)
    + Ключ - `tvm_secret`, значение - соответсвующий секрет
+ Даем доступы на чтения для людей из своей группы
+ Запрашиваем с указанием `--secret-id` и `--client`
    + Например,  `./bb_requester  --secret-id=sec-01dymkq44w07qaarm9x68a0gg6 --client morda-plus --uid 100500`
        + Не забываем про доступ к yav из консоли (ssh-agent или `--authorization`)
