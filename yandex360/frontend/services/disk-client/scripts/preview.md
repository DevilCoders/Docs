## Проксирования превьюшек ресурса для редактора

Из-за сложностей выкачивания редактором залогиновых превьюшек решено было сделать [специальную ручку в mpfs](https://wiki.yandex-team.ru/disk/mpfs/api/json#fotoredaktoraviary), которая выдаст такую ссылку на превью, по которой можно скачать изображение без кук. Запрос по этой ссылке происходит с использованием внутреннего редиректа в nginx, чтобы не палить ссылку в браузер.

Чтобы не палить эту ссылку в браузере, сделано проксирование с использованием внутреннего редиректа.

Схема следующая:

![](http://jing.yandex-team.ru/files/vitkarpov/2014-05-27_1540.png)

### Некоторые особенности

На самом деле mpfs отдает ссылку на балансер заберуна `downloader.disk.yandex.ru`. Если балансер делает 302 редирект в регион, то схема перестает работать: nginx проксирует в браузер 302 и запрос за картинкой делает браузер, а это совсем не то, что нужно.

Для того, чтобы отключить региональную программу в заберуне, можно делать запросы со специальным get-параметров `force_default=yes` — тогда картинку отдаст сам балансер напрямую.