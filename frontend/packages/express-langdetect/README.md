# express-langdetect

Это обертка над N-API модулем `langdetect`, которая определяет язык пользователя по перечню параметров.
Документация по `langdetect` лежит на [doc.yandex-team.ru](http://doc.yandex-team.ru/lib/lang-detect/concepts/lang-detect-descr.xml).

Использует N-API бининг [@yandex-int/langdetect](https://a.yandex-team.ru/arc/trunk/arcadia/mail/nodejs/js/langdetect).

## Important

Для работы нужен пакет с данными для langdetect:

 * `libyandex-lang-detect-data` — содержит файл lang-detect-data.txt

## Install

Set your npm registry server to `http://npm.yandex-team.ru` then npm install `@yandex-int/express-langdetect`

## Usage

```ts
import express from 'express';
import expressBlackbox from '@yandex-int/express-blackbox';
import expressLangdetect from '@yandex-int/express-langdetect';

const app = express();

app.use(express.cookieParser());
app.use(expressBlackbox({ api: 'blackbox-mimino.yandex.net' ));
app.use(expressLangdetect());

app.get('/', function (req) {
    console.log(req.langdetect); // {id: 'ru', name: 'Ru'}
});
```

> __Pro tip:__ Рекомендуем включать `trust proxy` для точного определения IP адреса пользователя: `app.enable('trust proxy');`

## API

### express-langdetect([options])

Возвращает middleware для express.

### options

#### availableLanguages
Type: `Function`, `Object`, `String`, `Array` Default: пустая строка

Языки, поддерживаемые приложением.

 * `Function`: Если передана функция - то она вызывается и результат ее работы интерпретируется как новый __availableLanguages__.

 * `Object`: Интерпретируется как соответствие доменов спискам доступных на этих доменах языков. Например:

```js
{
    'ru': ['ru'],
    'ua': ['ru', 'uk'],
    'by': ['ru', 'be'],
    'kz': ['ru', 'kk'],
    'com': ['en'],
    'com.tr': ['tr']
}
```

 * `Array`: Приводится к строке через `.join(',')`

 * `String`: Список доступных языков для приложения. Передается в параметер `filter` сервису `lang-detect`. Если язык пользователя (который определил `lang-detect`) не в этом списке, то будет использован язык по умолчанию (__defaultLanguage__).

> __Pro tip:__ Изучая [исходники lang-detect](https://a.yandex-team.ru/arc/trunk/arcadia/contrib/libs/lang_detect/library/lookup_impl.cpp) можно понять, что пустая строка в `availableLanguages` значит, что все языки доступны.

#### defaultLanguage
Type: `String`, `Array` Default: `ru`

Язык по умолчанию. Массив приводится к строке через `.join(',')`.

Применяется если:

 * В `availableLanguages` был объект с доменами и домен из запроса не был в нем найден.
 * Если `LangDetect.find` не смог ничего определить и вернул `undefined`
 * Согласно [описанию работы `lang-detect`](http://doc.yandex-team.ru/lib/lang-detect/concepts/lang-detect-descr.xml), так как передается как параметер `default`.

#### exposeLangdetector
Type: `Boolean` Default: `false`

Кладет в `req.langdetect.detector` ссылку на объект `LangDetector`.

#### list
Type: `Boolean` Default: `false`

Запрашивает список совместимых языков для пользователя и сохраняет их в `req.langdetect.list`. Например там может оказаться вот такой массив: `[ { id: 'ru', name: 'Ru' }, { id: 'uk', name: 'Ua' } ]`.

#### langDetectData
Type: `String` Default: `/usr/share/yandex/lang_detect_data.txt`

Путь до данных для lang-detect.
