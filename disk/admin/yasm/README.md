# Шаблоны в головане
https://yasm.yandex-team.ru

## Шаблоны панелей

Лежат в директории ./templates/
Для загрузки/обновления воспользоваться веб-интерфейсом, либо [API](https://wiki.yandex-team.ru/golovan/templatium/api/#api)

Обновить шаблон disk_mpfs: `curl --data-binary @templates/disk_mpfs.jinja2 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/update/content?key=disk_mpfs'`

## Шаблоны алертов

Лежат в директории ./alerts/
Для загрузки/обновления используется только [API](https://wiki.yandex-team.ru/golovan/alerts/api/)


### Создание шаблона алертов
Если шаблон еще не создан в yasm, нужно создать его: curl -d '{"key": "disk_uploader", "owners": ["m-messiah", "ivanov-d-s", "kolyann", "ignition", "bpsavelev"]}' 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/create'

### Порядок обновления алертов
1. Поправить шаблон в файле
2. Проверить рендеринг: `curl --data-binary @alerts/disk_mpfs.jinja2 https://yasm.yandex-team.ru/srvambry/tmpl/alerts/render_json/content`
3. Если все устраивает, то загрузить новую версию: `curl --data-binary @alerts/disk_mpfs.jinja2 https://yasm.yandex-team.ru/srvambry/tmpl/alerts/update/content?key=disk_mpfs`
4. Применить шаблон для генерации алертов: `curl -XPOST https://yasm.yandex-team.ru/srvambry/tmpl/alerts/apply/disk_mpfs` (перетрет все алерты с префиксом disk_mpfs.)

### Поиск алертов в головане
https://yasm.yandex-team.ru/search/-alerts/?term=disk_mpfs.

Где в term подставляется key шаблона.

### Как залить обновления через скрипт

# Заливаем алерты
./yasm_curl.sh a disk-awacs-balancers u ./alerts/disk-awacs-balancers.jinja2

# Применяем алерты
./yasm_curl.sh a disk-awacs-balancers a ./alerts/disk-awacs-balancers.jinja2

# Заливаем панель, применять не надо
./yasm_curl.sh p disk_zomb u ./templates/disk_zomb.jinja2

