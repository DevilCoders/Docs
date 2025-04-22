# User

Базовый модуль для получения информации о пользователе, его регионе, браузере и l10n-параметрах.

- [Версионирование](#%D0%92%D0%B5%D1%80%D1%81%D0%B8%D0%BE%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5)
- [Контрибьют](#%D0%9A%D0%BE%D0%BD%D1%82%D1%80%D0%B8%D0%B1%D1%8C%D1%8E%D1%82)
- [Функциональность](#%D0%A4%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D0%BE%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D1%8C)
- [Инициализация](#%D0%98%D0%BD%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F)
    - [Конфигурация](#%D0%9A%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D1%8F-%D1%84%D0%BE%D1%80%D0%BC%D0%B0%D1%82-config)
- [auth](#auth)
    - [Геттеры](#%D0%93%D0%B5%D1%82%D1%82%D0%B5%D1%80%D1%8B)
    - [Методы](#%D0%9C%D0%B5%D1%82%D0%BE%D0%B4%D1%8B)
- [browser](#browser)
    - [Геттеры](#%D0%93%D0%B5%D1%82%D1%82%D0%B5%D1%80%D1%8B-1)
        - [Поля из uatraits](#%D0%9F%D0%BE%D0%BB%D1%8F-%D0%B8%D0%B7-uatraits)
        - [Отдельно](#%D0%9E%D1%82%D0%B4%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE)
- [region](#region)
    - [Логика](#%D0%9B%D0%BE%D0%B3%D0%B8%D0%BA%D0%B0)
    - [Геттеры](#%D0%93%D0%B5%D1%82%D1%82%D0%B5%D1%80%D1%8B-2)
        - [Определившийся регион](#%D0%9E%D0%BF%D1%80%D0%B5%D0%B4%D0%B5%D0%BB%D0%B8%D0%B2%D1%88%D0%B8%D0%B9%D1%81%D1%8F-%D1%80%D0%B5%D0%B3%D0%B8%D0%BE%D0%BD)
        - [По произвольному id](#%D0%9F%D0%BE-%D0%BF%D1%80%D0%BE%D0%B8%D0%B7%D0%B2%D0%BE%D0%BB%D1%8C%D0%BD%D0%BE%D0%BC%D1%83-id-number)
        - [По произвольным ids](#%D0%9F%D0%BE-%D0%BF%D1%80%D0%BE%D0%B8%D0%B7%D0%B2%D0%BE%D0%BB%D1%8C%D0%BD%D1%8B%D0%BC-ids-number)
        - [Дополнительно](#%D0%94%D0%BE%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE)
    - [Сеттеры](#%D0%A1%D0%B5%D1%82%D1%82%D0%B5%D1%80%D1%8B)
- [l10n](#l10n)
    - [Геттеры](#%D0%93%D0%B5%D1%82%D1%82%D0%B5%D1%80%D1%8B-3)
    - [Сеттеры](#%D0%A1%D0%B5%D1%82%D1%82%D0%B5%D1%80%D1%8B-1)
    - [Дополнительно](#%D0%94%D0%BE%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE-1)
- [role](#role)
    - [Методы](#Методы-1)
    - [Дополнительно](#Дополнительно-2)
    - [Пример](#Пример)
- [Подключение собственных компонент](#%D0%9F%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-%D1%81%D0%BE%D0%B1%D1%81%D1%82%D0%B2%D0%B5%D0%BD%D0%BD%D1%8B%D1%85-%D0%BA%D0%BE%D0%BC%D0%BF%D0%BE%D0%BD%D0%B5%D0%BD%D1%82)
- [Внешние зависимости](#%D0%92%D0%BD%D0%B5%D1%88%D0%BD%D0%B8%D0%B5-%D0%B7%D0%B0%D0%B2%D0%B8%D1%81%D0%B8%D0%BC%D0%BE%D1%81%D1%82%D0%B8)

## Версионирование

Модуль использует [semver](http://semver.org/), версии фиксируются тегами.
Совместимость гарантируется только для публичного интерфейса модуля (инициализация и геттеры).

## Контрибьют

PR в ветку `master`.
Ревьюеры: @kaero, @varankinv, @flack, @orion, @an9eldust

## Функциональность

Модуль выполняет следующие задачи:

* доступ к информации из Паспорта,
* обновление кук `Session_id` и `yandexuid`,
* генерация и валидация секретного ключа,
* МДА-авторизация,
* доступ к информации о браузере,
* доступ к данным о регионе пользователя (включая транслокальность Крыма),
* доступ к данным о настройках локализации.

## Инициализация

Асинхронный вызов на vow-промисах.

```javascript
var User = require('nodules-user');

return new User(req/*{http.IncomingMessage}*/, res/*{http.ServerResponse}*/, config/*{Object}*/)
    .init('browser')
    .init('role')
    .then(function(user) {
        return user.init('auth');
    })
    .then(function(user) {
        return user.init('region');
    })
    .then(function(user) {
        return user.init('l10n');
    })
    .then(function(user) {
        req.user = user;
        return;
    });
```

Важно понимать, что очередность инициализации не является произвольной. Зависимости следующие:

* `browser` не имеет зависимостей;
* `role` не имеет зависимостей;
* `region` не имеет зависимостей;
* `l10n` зависит от `auth` и `region`;
* при инициализации `l10n`, `region` будет возвращать данные с учётом языка.

Модули должны быть не только инициализованы, но и заданы в `config`, см. ниже.

Неинициализированные модули не будут выполняться и не окажут влияния на рантайм приложения.

### Конфигурация (формат `config`)

Включенными считаются те модули, для которых значение ключа установлено в `Object` (при установке пустого объекта будут использованы дефолтные параметры).

Список параметров и значения по умолчанию смотрите в [Config.defaultConfig](https://github.yandex-team.ru/nodules/user/blob/master/lib/config.js).

## `auth`

### Геттеры

* `{String} crc` секретный ключ
* `{String} yandexuid` значение куки yandexuid или пустая строка
* `{String} uid` uid пользователя или пустая строка
* `{String | null} ticket` аутентификационный тикет выписанный [TVM](https://wiki.yandex-team.ru/passport/auth-tokens/).
  Необходимость получения тикета конфигурируется полем `config.auth.getAuthTicket`.
* `{String} login` login или пустая строка
* `{Object | null} redirect` флаг обозначающий, что пользователя нужно перенаправить к pass для копиросания кук в МДА.
  Адрес pass-сервера описывается в поле `redirect.location`
* `{Boolean} isAuth` флаг авторизованного пользователя (имеющего uid)
* `{Boolean} isSocialUser` флаг пользователя с соц.авторизацией
* `{Boolean} isLiteUser` учетная запись, зарегистрированная на Моем Круге по упрощенной схеме, с указанием только электронного адреса и пароля.
* `{Boolean} isLiteAuth` пользователь с автологинящей ссылки из письма Моего Круга
* `{Boolean} isHostedUser` пользователь ПДД
* `{Boolean} isBetaTester` бета-тестер (668 сид)
* `{Boolean} isYandexEmployee` сотрудник Яндекса (669 сид)
* `{Boolean} isNeedRedirectToMobile` необходимость редиректа на мобильную версию. По сути проверяет настройку из 44-го блока куки `my`
* `{Number} testingGroup` группа от 0 до 9, используемая для экспериментов, берётся из `yandexuid`
* `{Object[]} emails` массив объектов, описывающих email'ы пользователя в формате:
  `{ address: String, validated: Boolean, default: Boolean, prohibit-restore: Boolean, rpop: Boolean, unsafe: Boolean, native: Boolean, born-date: String }`
* `{String} passLang` предпочитаемый пользователем язык интерфейса при регистрации или пустая строка.
* `{Object|null} name` возвращает объект с `display_name` из Паспорта.
* `{Object} type` для залогинов возвращает: `{ kind : 'uid', id : uid }`, для незалогинов: `{ kind : 'cuid', id : yandexuid }`.
* `{Boolean} blackboxRequestFailed` имеет значение `true`, если не удалось получить ответ от ЧЯ, если ответ пустой или не удалось распарсить JSON.

### Методы

* `{Boolean} checkCRC({String} crc)` возвращает булев флаг проверки секретного ключа
* `{String} dbField({String} field)` Поля из базы паспорта (должны быть прописаны в конфиге `User`)
* `{String} attribute({String|Number} attrName)` Аттрибут из базы паспорта (должны быть прописаны в конфиге `User`)
* `{String} alias({String|Number} aliasName)` Алиас для пользователя из базы паспорта (должны быть прописаны в конфиге `User`)

### Статические методы

* `{Function} Auth.my({http.IncomingMessage})` возвращает функцию `{Number|undefined} ({String|Number} block, {Number} [index=0])` для получение значения определенного блока куки my
* `{Boolean} Auth.isNeedRedirectToMobile({http.IncomingMessage})` аналог динамического геттера

## `browser`

### Геттеры

#### Поля из uatraits

Динамические геттеры на все поля, [предоставляемые uatraits](http://wiki.yandex-team.ru/Morda/browserDetect).

Значения нормализуются в более подобающие (`'true'` -> `true`, `'false'` -> `false`, `'undefined'` -> `undefined`).

#### Отдельно

Для удобства эти поля возвращаются всегда, для десктопов в соответствующих геттерах будет `false`.

* `{Boolean} isOld` флаг о том, что у пользователя IE <=7 версии или Опера <= 10 версии.
* `{Boolean} isMobile` мобильное устройство
* `{Boolean} isTouch` тачевый телефон
* `{Boolean} isTablet` планшет

Для тачфонов в `true` будут выставлены и `isMobile`, и `isTouch`. А для планшетов `true` отдадут все три свойства.
Например, для редиректа на мобильную версию можно использовать проверку `isMobile && ! isTablet`.

Список устаревших браузеров (`isOld = true`) можно переопределить с помощью опции `oldBrowsers` конфига:
```
    browser: {
       oldBrowsers: [
           { name: 'MSIE', version: 9 },
           { name: 'Opera', version: 11 }
       ]
    }
```

## `region`

### Логика

Модуль определяет несколько самостоятельных, но различающихся по приоритету источников данных для выяснения региона запроса.
Для каждого из источников определение региона происходит отдельно.
По умолчанию возвращается регион из источника с максимальным приоритетом, однако и все остальные также доступны.

| Источник                     | `source`          | Пример выставления                  | Пример получения                      |
| ---------------------------- | ----------------- | ----------------------------------- | ------------------------------------- |
| Переопределение `EXTRA`      | 50                | `setId(2, region.SOURCES.EXTRA)`    | `idBySource(region.SOURCES.EXTRA)`    |
| Из урла `URL`                | 40                | `setId(2, region.SOURCES.URL)`      | `idBySource(region.SOURCES.URL)`      |
| Настройки сервиса `SETTINGS` | 30                | `setId(2, region.SOURCES.SETTINGS)` | `idBySource(region.SOURCES.SETTINGS)` |
| Портальный регион `DETECTED` | 20                | `setId(2, region.SOURCES.DETECTED)` | `idBySource(region.SOURCES.DETECTED)` |
| Дефолтный `DEFAULT`          | 10                | `setId(2, region.SOURCES.DEFAULT)`  | `idBySource(region.SOURCES.DEFAULT)`  |

* портальный регион включает в себя и определение по ip (по аналогии с `geo-block`'ом `xscript`);
* для `URL` требуется передача в конфиг правильных `url` и `region.regionParamName`;
* регионы с источниками `EXTRA` и `SETTINGS` выставляются только на стороне сервиса;
* `DEFAULT` берётся из конфига `region.defaultId`.

### Геттеры

**Важно: При использовании `l10n` информация предоставляется с учётом языка.**

#### Определившийся регион

* `{Number} id` идентификатор определённого региона. При нескольких регионах (напр. в урле) берётся первый.
* `{Number[]} ids` массив идентификаторов определенных регионов. При нескольких регионах (напр. в урле) возвращаются все.
* `{String} name` имя региона в именительном падеже. При нескольких регионах берётся первый.
* `{String[]} names` массив имён регионов в именительном падеже.
* `{Number} portalId` регион из настроек.
* `{Number} urlId` id регион из урла. В случае нескольких вернётся первый.
* `{Number[]} urlIds` массив id регионов из урла.
* `{Object} linguistics` возвращает имя региона во всевозможных падежах.
* `{Number} country` возвращает id страны, в которую входит текущий регион.
* `{Object} info` объект с полной информацией об определившемся регионе, включает `id`, `name`, `country`, `linguistics` и `data` (результат ответа [regionById](https://wiki.yandex-team.ru/rimzaidullin/libgeobase3/libgeobase3-nodejs-api#regionbyid)).
* `{Object} timezone` возвращает информацию о часовом поясе текущего региона (результат ответа [tzinfo](http://doc.yandex-team.ru/face/libgeobase/concepts/interfaces-nodejs.xml#meth-tzinfo)).

#### По произвольному id `{Number}`

* `{Object} infoById` объект с полной информацией о регионе, включает `id`, `name`, `country`, `linguistics` и `data` (результат ответа [regionById](https://wiki.yandex-team.ru/rimzaidullin/libgeobase3/libgeobase3-nodejs-api#regionbyid)).
* `{String} nameById` имя региона в именительном падеже.
* `{Object} linguisticsById` возвращает имя региона в различных падежах.
* `{Object} timezoneById` возвращает информацию о часовом поясе региона (результат ответа [tzinfo](http://doc.yandex-team.ru/face/libgeobase/concepts/interfaces-nodejs.xml#meth-tzinfo)).

#### По произвольным ids `{Number[]}`

* `{String[]} namesByIds` возвращает массив имён регионов в именительном падеже.

#### Дополнительно

* `{Boolean} idIsIn ({Number} id, {Number} parentId)` проверяет принадлежность региона с идентификатором rid региону с идентификатором parentRid
* `{Number} source` источник, по которому определён регион
* `{Object} SOURCES` список всех источников
* `idBySource({Number})` возвращает id региона `{Number}` из источника `source`
* `idsBySource({Number})` возвращает id регионов `{Number[]}` из источника `source`
* `{Boolean|null} isInternalNetwork` проверяет принадлежность IP юзера к внутренней сети

### Сеттеры

В некоторых случаях нужно установить регион прямо в середине рантайме (напр. когда бекенд опознал регион в текстовом поисковом запросе).

* `setId({Number})` устанавливает id региона. Вторым аргументом можно передать нужный `source {Number=50}`.
* `setIds({Number[]})` устанавливает несколько id регионов. Вторым аргументом можно передать нужный `source {Number=50}`.

Этот регион становится текущим для запроса.

## `l10n`

Понятие "источник" при определении локализации несет [ту же смысловую нагрузку](#%D0%9B%D0%BE%D0%B3%D0%B8%D0%BA%D0%B0), что и при определении региона.

Интерфейс у `locale`, `lang` и `currency` одинаков.

Если валюты не нужны, не задавайте их в `config`, `currency` не будет инициализироваться.

### Геттеры

* `{String} *.id` значение определившегося параметра
* `{String[]|{Object[]}} *.list` список допустимых значений. `{Object[]}` для `lang`.
* `{String} *.default` дефолтное значение

### Сеттеры

* `*.setId({String})` устанавливает id соответствующего параметра. Вторым аргументом можно передать нужный `source {Number}`.

### Дополнительно

* `{Number} *.source` источник, по которому определён соответствующий параметр
* `{Object} *.SOURCES` список всех источников
* `*.idBySource({Number})` возвращает значение `{String}` по источнику `source`

## `role`

Компонент для работы с ролями пользователя. Является необязательным компонентом. Служит для авторизации пользователей.

Роли для пользователя задаются на этапе инициализации, с помощью полученной из конфига функции `getRoles({Function} callback)`. Каждой роли соответствует определённый набор прав. Наборы прав для ролей описываются в конфиге, в хэше `roles`.

Конфиг:
```js
role : {
    /**
     * Список ролей пользователей со списком соответствующих прав
     * @type {Object}
     */
    roles : {
        READER : [ 'COMMENT_READ' ],
        WRITER : [ 'COMMENT_READ', 'COMMENT_WRITE' ]
    },

    /**
     * Получает роли пользователя и передаёт в callback
     * @type {Function}
     * @param {Funtion} callback Первым аргументом - ошибка, вторым - результат.
     */
    getRoles : function(callback) {
        callback(null, []);
    }
},
```

Далее для авторизации следует использовать метод `hasAccess({Number} флаги из ACCESS)`, который проверяет наличие необходимых прав доступа у пользователя. Все возможные права доступа хранятся в хэше `ACCESS`. Пример использования смотрите ниже.

### Методы

* `{Boolean} hasAccess({Number} флаги из ACCESS)` Проверяет права пользователя. Для проверки следует использовать флаги прав из `ACCESS`.

### Дополнительно

* `{Object} ACCESS` Список всех возможных прав пользователя.
* `{Object} ROLES` Список всех возможных ролей пользователя.

### Пример

```js
var role = user.role;

if(role.hasAccess(role.ACCESS.COMMENT_WRITE | role.ACCESS.COMMENT_READ)) {
    doSomething();
}
```

## Подключение собственных компонент

Для подключения собственных компонент, модуль предоставляет статический метод `User.registerComponent`.

### Пример

```js
var User = require('nodules-user'),
    OAuth = require('nodules-user-oauth');

User.registerComponent('oauth' /* {String} name */, OAuth /* {Object} componentCls */);

return new User(req, res, config).init('oauth');
```

Внешний компонент обязан быть зарегистрирован в модуле до инициализации.

Пример внешних компонент:

* [nodules-user-oauth](https://github.yandex-team.ru/nodules/user-oauth).

### Указание конфига для компонента
```javascript
function RegionAsync(user, config) {
    this._user = user;
    this._driver = config.driver;
}
// ...
User.registerComponent('regionAsync', RegionAsync, {
    driver: driver
});
```

## Внешние зависимости

* [connect](http://www.senchalabs.org/connect/) или [express](http://expressjs.com/)
* [vow](https://github.com/dfilatov/jspromise) или совместимая реализация
* `uatraits-nodejs-0.10 >= 14.0-uatraits-1.2.0-2`
* `geobase4-nodejs-0.10 >= 14.0-geobase4-4.1-36`
* `langdetect-nodejs-0.10 >= 14.0-langdetect-1.6-20`
