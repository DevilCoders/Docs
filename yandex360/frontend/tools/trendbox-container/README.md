Trendbox LXC container
======================

## Focal mode

Трендбокс закапывается и поддержки нет. Но хочется собираться на фокале.
Собрал фокал тут: https://sandbox.yandex-team.ru/task/1271422407/view
Ресурс: https://sandbox.yandex-team.ru/resource/2967194243/view

Т.е. для сборки нового контейнера, можно сдублировать эту таску и вставить
в `Shell script to execute during final stage` содержимое `custom_script.sh`.


## Xenial- mode

Для сборки следуем [документации][1].

Ставим галочки `node_js`, `docker`.

Добавляем в Pre-install Node.js versions
```json
[{"npm":"6.14.1","node_js":"8.12.0"}]
```
по желанию можно добавить ещё версий ноды.

В поле `Shell script...` добавить содержимое файла `custom.sh`.

После сборки стоит протестировать контейнер и если всё хорошо,
то добавить ему атрибут `status=stable`.

[Список собранных контейнеров][2].


  [1]: https://github.yandex-team.ru/search-interfaces/trendbox-ci/blob/master/docs/formats/0.2/recipes/build-lxc.md
  [2]: https://sandbox.yandex-team.ru/resources?owner=PS-FRONTEND&type=TRENDBOX_CI_LXC_IMAGE_BETA&limit=20&created=6_months
