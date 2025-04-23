Внесение изменений
============

Изменение mandrel и их проверка
----------------------------------------

*Важно:* `.js.flow` нужно именить руками, внеся те же правки что и в основной код. На сборку в мономаркете это никак не влияет, но маркетфронт с некорректным flow упадёт.

На время разработки можно слинковать 2 проекта симлинками:
* ставим `node_modules` в marketfront и собираем
* в директории с маркетфронтом удаляем `rm -rf node_modules/@yandex-market/mandrel`
* собираем `mandrel`
* делаем симлинк `ln -s /var/lib/yandex/monomarket/<login>/lib/lib/mandrel/dist var/lib/yandex/marketfront/<login>/node_modules/@yandex-market/mandrel`
