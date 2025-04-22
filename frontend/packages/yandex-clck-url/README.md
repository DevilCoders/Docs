# yandex-clck-url [![Build Status](http://drone-beta.haze.yandex.net/api/badges/project-stub/yandex-clck-url/status.svg)](http://drone-beta.haze.yandex.net/project-stub/yandex-clck-url) [![OKO health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend/packages/yandex-clck-url&vcs=arc)](https://oko.yandex-team.ru/repo/toolbox/yandex-clck-url)

Клик-демон нужен для учета кликов по ссылкам Вашего проекта. Обычный переход по ссылке с http на https теряет referrer, а клик-демон его сохраняет. Также возможно передать параметры перехода.

Существует, как минимум, 2 типа ссылок:

1. Без шифрования – можно использовать только для переходов между сервисами Яндекса
2. С шифрованием – для выполнения переходов на любой адрес

В данном модуле реализована генерация вышеперечисленных типов ссылок.

[Wiki демона](https://beta.wiki.yandex-team.ru/Clickdaemon/) | [Проверка url](https://weather-ci.common-ext.yandex-team.ru/clck)

## Usage:

```js
var Clck = require('yandex-clck-url');

var clck = new Clck();
clck.getClickUrl('https://beta.maps.yandex.ru/-/CVCz7OoI');
//clck.yandex.ru/redir/*data=url=https%3A%2F%2Fbeta.maps.yandex.ru%2F-%2FCVCz7OoI

var clck = new Clck({
  key: 'W50/PxLsdRldOKXKklW4Ng==',
  keyNo: 5,
  crypt: 2,
  params: {
    dtype: 'stred',
    ab: true
  },
  yandexuid: 111
});
clck.getClickUrl('http://www.kinopoisk.ru/docs/usage/');
//clck.yandex.ru/redir/0aFDX7JeDaa-KKccW2PFEryNUAwbxzzE?data=b1hYYzE3QzQ3RFNRbDFIZWxVZExDY1BRODNNTXFBeHdlQVFtUm1SS2ZPWEFacnRGNTNCQlpiMFdvazFGTnhXcEowM0E1c1VwbEtXU2RnZzk5SlprNHYzcC02U1ZNWmJCbVFJZW1EYy15ZDQ&b64e=2&sign=773a391054ecf10f7feaeb15805d7039&keyno=5

var clck = new Clck({ key: 'jQm9NqfREKGKRNgHSGLV1A==' });
clck.decrypt('P8Xe6bY5djotfrl5g6OiJQ,,')
// 37093,0,72

var clck = new Clck({ key: 'jQm9NqfREKGKRNgHSGLV1A==' });
clck.encrypt('37093,0,72')
// P8Xe6bY5djotfrl5g6OiJQ,,
```


## API

### Clck([options])

Возвращает экземпляр класса Clck с доступными методами.

#### Методы

Доступные методы:

##### getClickUrl
Генератор ссылок

##### sign
Подпись

##### decrypt
Расшифровка данных

##### encrypt
Шифрование данных

#### Options

Объект с опциями:

##### key
Type: `String` или `Buffer`

Ключ для шифрования.

Если тип `String`, то ключ будет преобразован к `base64`. Для оптимизации производительности (+500 Op/s) можно сразу передать `Buffer.from('yourkey', 'base64')`.

Используется в паре с `keyNo`.

##### keyNo
Type: `Number`

Номер ключа для шифрования.

Используется в паре с `key`.

##### crypt
Type: `Number`
Default: `0`

Версия шифрования:

 * `0` - Без шифрования
 * `2` - Шифрование с использованием `key` и `keyNo`

##### params
Type: `Object|String`
Default: `*`

Параметры в виде объекта.

Возможна прямая передача в виде строки: `params: 'dtype=stred/ab=true/*'` (`*` в конце строки __обязательна__).

##### yandexuid
Type: `Number`

yandexuid пользователя, подписывающего ссылку

##### host
Type: `String`
Default: `//clck.yandex.ru`

Адрес клик-демона.

##### referrer
Type: `String`

Параметр, по которому можно было бы однозначно понять, откуда пришел человек. Полезен для построения отчетов сервисами.

##### jsredir
Type: `Boolean`
Default: `false`

Использовать jsredir. `http://clck.yandex.ru/jsredir?state=...`. Подробнее: https://wiki.yandex-team.ru/alexanderloukianov/https

##### extParams
Type: `Object`

Набор произвольных параметров.

## Ключи
Ключи живут [тут](https://a.yandex-team.ru/arc/trunk/arcadia/serp/mobile/core/src/main/resources/resources/clickdaemon.keys.txt?rev=2099533).
key и keyNo должны соответствтовать тому, что есть в файле. Если вдруг что-то сломалось, нужно проверить, не обновился ли файл.
Вопросы, связанные с ключами, можно задавать [mishgun@](http://staff.yandex-team.ru/mishgun).
