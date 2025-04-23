## MAIL-TOOL
Утилита для отправки специализированных сообщений.
Например, написать письмо от имени рассылки.

1. Зайти на dev-тачку (а-ля spica.maps.dev.yandex.net или jakku)
2. Проверить доступ до почтового сервера: `telnet yabacks.mail.yandex.net 25`
3. Собрать mail-tool
4. Создать свои файлы subject.txt, text.txt
5. Скопировать config.example.json в config.json
6. Скопировать в текущий каталог вложения
7. Исправить config.json, исправив from, to, файлы к subject/text и список вложений
8. Запустить: `./mail-tool --config config.json`
