Конвертирование данных:
data/convert.pl deputats.xlsx > deputats1.js
data/grap_images.pl deputats1.js images/deputats > deputats.js
rm data/deputats1.js

Аналогично для senatots

Файлы могут быть большого размера, пережимаем вручную (сейчас deputats/5a212c4f9ef2615953f8c1766f6d7ed5.jpg)
http://www.picresize.com/

Сборка всего (html, css, js):
make all

Сборка без npm
make grunt
