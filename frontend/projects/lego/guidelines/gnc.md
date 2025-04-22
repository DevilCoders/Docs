## Инструкция по заведению сервисов в колокольчике

- [Общая информация](#Общая-информация)


1. Заливка иконок
   - Формат иконки: SVG 42х42 пикселя
   - Залить в аватарницу - `ya_notification_center` 
   - Для заливки картинок нужна дырка к avatars-int.mds.yandex.net:13000. 
   - Сохранить иконку локально, потом копируем ее в свою директорию на рабочей машине
   
    `scp Downloads/icon_main.svg imgrover8.search.yandex.net:~/`

Завести отдельный keyset в танкере для нового сервиса

https://tanker.yandex-team.ru/?project=disk_notifiier&branch=master

2. Добавление сервиса 

https://notifier.dst.yandex-team.ru/z/notifier-types — тестовая база
https://notifier.disk.yandex-team.ru/z/notifier-types — production

- Начинаем с тестовой базы
- Сначала заводим сервис, путь до иконки, название сервиса
- Группы нотификаций
- Заводим кейсеты в Танкере https://tanker.yandex-team.ru/?project=disk_notifiier&branch=master
- Заводим конкретные нотификации в тестовой базе колокола
- на вкладке Notifier Types нажимаем кнопку Update Tanker Cache


Можно отправлять тестовые сообщения
- `curl -v -X POST "http://api-stable.dst.yandex.net:8080/v1/notifier/service/add-notification?service=music&uid=4016610198&actor=ya_music&type=daily_created&meta=%7B%22username%22%3A%20%7B%22type%22%3A%20%22text%22%2C%20%22text%22%3A%20%22%D0%94%D0%B5%D0%BD%D0%B8%D1%81%22%7D%7D"`
- music,
- ya_music,
- посмотреть uid из тестового Паспорта (https://pass-test.yandex.ru/blackbox?method=userinfo&login=<login>&userip=127.0.0.1 ), 4016610198
- мета-информация — нужно сформировать json и encodeURI его http://urlencode.org  
`{"username": {"type": "text", "text": "Денис"}}`
- дальше проверяем отправку на примере



http://notifier-1.notifier.testing.disk-notifier.disk.stable.qloud-d.yandex.net:51979/z/notifier-types
