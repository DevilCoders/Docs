# Url ресурса

`sbr:<sandbox resource id>` позволяет скачать ресурс из Sandbox, указав его ID с помощью торрентов. Время жизни ресурса будет продлеваться автоматически пока ресурс используется.

`rbtorrent:<torrent id>` позволяет скачать торрент по его ID, но следить за жизнью сидеров придётся самостоятельно.

`http`, `https` позволяет скачать произвольный файл, но нужно помнить что:
* нужны соответствующие правила в firewall;
* более высокая нагрузка на сервер, раздающий файлы по http;
* нет гарантии (не указывая `checksum`) что разные скачивания файла не приведут к разному содержимому этого файла.
