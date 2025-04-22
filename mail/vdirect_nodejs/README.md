# Что это
Биндинг функций хеширования vdirect в ноду. Функция *createHashForUidLink* создаёт хеш для урла и юида, функция *validateHashForUidLink* проверяет правильность хеша для юида и урла

# Содержимое пакета
```
$ dpkg -L yandex-mail-vdirect-nodejs
/.
/usr
/usr/lib
/usr/lib/vdirect
/usr/lib/vdirect_nodejs
/usr/lib/vdirect_nodejs/vdirect.node
/usr/lib/vdirect_nodejs/libvdirect_nodejs.so.0.0
/usr/share
/usr/share/doc
/usr/share/doc/yandex-mail-vdirect-nodejs
/usr/share/doc/yandex-mail-vdirect-nodejs/copyright
/usr/share/doc/yandex-mail-vdirect-nodejs/changelog.gz
/usr/lib/vdirect_nodejs/libvdirect_nodejs.so.0
```

# Установка
1. Поставить пакет *yandex-mail-vdirect-nodejs*
2. Добавить в скрипт запуска nodejs переменную *LD_LIBRARY_PATH*, в которой указать путь до *libvdirect_nodejs.so*, указать переменную *NODE_PATH*, в которой указать путь до *vdirect.node*
3. На машине должен быть файл `.vdirectkeys`, на кластере @mail_web он лежит по адресу `/home/wmi/.vdirectkeys`

# Использование
## Создание объекта
```javascript
var vdirect_module = require('vdirect');
var vdirect = vdirect_module.Vdirect(path_to_vdirect_keys());
```
## Создание хеша
```javascript
const UID = "123";
const URL = "http://ya.ru"
var HASH = vdirect.createHashForUidLink(UID, URL);
```
## Проверка хеша
```javascript
const UID = "123";
const URL = "http://ya.ru"
const HASH = "asdf";
if (vdirect.validateHashForUidLink(UID, URL, HASH)) {
    console.log("ok");
} else {
    console.log("ne ok");
}
```

## Исключения
[Смотри в юниттесты](https://github.yandex-team.ru/mail/vdirect_nodejs/blob/master/vdirect/tests/test.js)

