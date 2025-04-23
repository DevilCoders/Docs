# i-global

**Статус блока**: **deprecated**

Рекомендуется перейти с использования блока в шаблонах и js к явной передаче параметров в BEMJSON, поскольку применение глобальных переменных является анти-паттерном и существенно увеличивает риск возникновения ошибок, а также существенно усложняет тестирование блоков.

Блок `i-global` содержит набор глобальных параметров – общие данные для проектов Лего. Предназначен для передачи значений параметров в контекст шаблонизатора и в JS-параметры блока [b-page](../b-page/b-page.ru.md).

Блок позволяет:

- настроить значения глобальных [параметров](#params) в BEMJSON блока `i-global` или в шаблонах блока (BEMHTML/BH) на проектном уровне;
- указать параметры, которые станут [доступны](#method-makePublic) для клиентского JavaScript проекта.


## Обзор блока

[Добавление и переопределение параметров](#init-params)<br>
[Получение значения параметров](#get-params)<br>
[Установка публичных параметров](#method-makePublic)


<a name="fields"></a>
### BEMJSON-поля блока
|  Поле | Тип | Описание |
| ----- | --- | -------- |
| [params](#fields-params) | Object | Глобальные параметры. |
| [reset](#fields-reset) | Boolean | Сброс значений глобальных параметров, переданных блоку через поле `params`. Значение по умолчанию: `true`. |

<a name="params"></a>
### Параметры блока

>Все перечисленные в таблице параметры переопределяемые. По умолчанию [доступны](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/i-global/i-global.bemhtml.js#L18) в клиентском JavaScript (кроме `show-counters-percent` — устанавливается в JS).


Параметр | Тип | Значение по умолчанию | Описание
-------- | --- | --------------------- | --------
`id` | String | — | **Обязательный**. Идентификатор сервиса Яндекса. В большинстве случаев совпадает с идентификатором из библиотеки Лего, который хранится в блоке [i-services](../i-services/__uri/i-services__uri.assets/source.json). Используется для доступа к информации о сервисе c учетом локализации.
`sid` | String | — | Идентификатор ([SID](https://doc.yandex-team.ru/Passport/AuthDevGuide/concepts/SID_About.xml)) сервиса, [зарегистрированного в паспорте](https://beta.wiki.yandex-team.ru/passport/sids/).
`lang`| String | `ru` | Язык контента.
`tld`| String | `ru` | Домен верхнего уровня. Используется для автоматической генерации хостов вида `yandex.[tld]`.
`content-region` | String | `ru` | Регион контента. Определяет содержимое сервиса/страницы/блока.
`user-region` | String | — | Регион пользователя. Накладывает ограничения на контент, показываемый пользователю.
`login` | String | `''` | Логин авторизованного пользователя Яндекса. По умолчанию будет взят из cookie (при наличии).
`displayName` | String | — | [Имя пользователя](https://doc.yandex-team.ru/blackbox/reference/method-userinfo-response-json.xml#display-name) для отображения в интерфейсе.
`index` | String | — | Параметр для главной страницы сервиса. Необходимо передать, чтобы удалить ссылку с логотипа сервиса.
`yandexuid` | String | — | Значение cookie `yandexuid`. Обязательно передавать любому пользователю.
`passport-host` | String | `https://passport.yandex.ru` | Адрес для изменения пути к сервису [Паспорт](https://passport.yandex.ru/).
`pass-host` | String | `https://api.passport.yandex.ru` | Адрес серверной части  Паспорта. Используется для получения информации от сервера (например, для обновления сессии пользователя в блоке [i-update-session](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/packages/islands/common.blocks/i-update-session/i-update-session.ru.md) или получения [списка сервисов](https://github.yandex-team.ru/lego/islands/blob/v4.x/common.blocks/i-services/__uri/i-services__uri.bemhtml.js)). Связан с параметром `passport-host`: при переопределении `passport-host`, необходимо переопределить и `pass-host`.
`passport-msg` | String | — |ID сервиса, c которого пользователь осуществляет вход или регистрирует учетную запись Яндекса на Паспорте. Используется для перенаправления пользователя на версию Паспорта данного сервиса (параметр `msg` в ссылке `passport?mode=register&msg=direct`) .
 `static-host` | String | — | Адрес хоста, c которого подключается статика.
 `lego-static-host`| String | `https://yastatic.net/lego/2.10-142` | Адрес статического хоста библиотеки [romochka](http://2-10.lego.yandex-team.ru/), с которого будут подключаться необходимые ресурсы нужной версии. Используется в блоках [b-head-stripe](../../desktop.blocks/b-head-stripe/b-head-stripe.ru.md), [b-keyboard](../../desktop.blocks/b-keyboard/b-keyboard.ru.md), [b-keyboard-loader](../../desktop.blocks/b-keyboard-loader/b-keyboard-loader.ru.md) и [i-clipboard](../../desktop.blocks/i-clipboard/i-clipboard.ru.md).
`social-host` | String | `https://social.yandex.ru` | Адрес хоста [социального профиля](https://doc.yandex-team.ru/Passport/AuthDevGuide/concepts/accounts-attributes.xml#social-profile) пользователя.
`clck` | String | — | Префикс адреса в счетчиках. Используется в SERP.
`click-host` | String | `//clck.yandex.ru` | Адрес хоста, на котором обрабатываются клики.
`export-host` | String |  `https://export.yandex.ru` | Адрес хоста, на котором [определялось](https://st.yandex-team.ru/ISL-1153) количество непрочитанных писем пользователя.
`i-host` | String | — | Адрес страницы авторизации, если текущий доменом отличен от `com` или `com.tr`. Использовался в блоке [b-head-user](https://github.yandex-team.ru/lego/romochka/blob/dev/blocks-desktop/b-head-user/b-head-user.js#L96).
`social-retpath` | String | — | Абсолютный адрес, на который следует перенаправить пользователя после успешной социальной авторизации.
`lego-path` | String | — | Путь к библиотекам Лего относительно корня проекта. По умолчанию: `/lego`.
`retpath` | String | — | Адрес, на который следует перенаправить пользователя после завершения аутентификации. По умолчанию текущая страница. Если параметр не указан, пользователь перенаправляется на страницу Паспорта.
`uid` | String | — | [UID](https://doc.yandex-team.ru/Passport/AuthDevGuide/concepts/Account_About.xml) аккаунта пользователя Яндекса.
`show-counters-percent` | Number | 100 | Процент срабатывания счетчиков `Lego.ch()`.|


### Методы блока

| Метод | Тип возвращаемого значения| Описание |
| --- | ------------------------- | -------- |
| [isPublic(param)](#method-isPublic) | Boolean | Проверяет доступность передаваемого параметра `param` в браузере. |
| [makePublic(param, flag)](#method-makePublic)| — | Делает переданный параметр `param` (или набор параметров переданных в виде `{param: true}`) доступным в браузере. Создан для замены  специализированной моды `public-params` (islands 3.х и ниже). |


## Подробнее

<a name="init-params"></a>
### Добавление и переопределение параметров

Способы добавления нового глобального параметра на уровне проекта или переопределение значения уже существующего:

- [На этапе инициализации шаблонизатора](#init)
- [На этапе передачи параметра в BEMJSON](#bemjson)

<a name="init"></a>
#### На этапе инициализации шаблонизатора

> **NB**  Значения параметров сохраняются при выставлении поля [reset в значение true](#fields-reset).

<!--[oninit()](#method-oninit) | –  | Определяет значения глобальных параметров при инициализации шаблонизатора BEMHTML. -->

Способ используется для глобальных параметров, которые одинаковы для конкретного сервиса и не уникальны для пользователя
(например, `sid`, `passport-host`). Значения таким параметрам устанавливаются один раз в глобальной переменной при инициализации
шаблонов (`onitit()` в BEMHTML или `function(bh){}` в BH). Это можно сделать на уровне сервиса в шаблонах блока `i-global`или в шаблонах
своего блока с добавлением `i-global` в mustDeps-зависимости.

> **NB** Глобальную переменную **не рекомендуется** переопределять полностью
 (`exports.BEMContext['i-global']` в BEMHTML  и `bh.lib.global` в BH). Следует переопределять отдельные свойства, указав их значения. Глобальная переменная может кэшироваться в других блоках, поэтому у них не будет доступа к значениям переопределенных параметров.

* В **BEMHTML** параметры необходимо указывать в переменной `exports['i-global']` глобальной функции
шаблонизатора BEMHTML – [oninit()](https://ru.bem.info/technology/bemhtml/v2/templating/#Добавление-пользовательских-методов-к-контекстно-независимым-полям), которая позволяет выполнить код один раз при инициализации шаблонов.

```javascript
oninit(function(exports) {
    var glob = exports['i-global'];
    glob.id = 'auto';
    glob.environment = 'development';
    glob.isDebug = true;
    glob.version = 1;
});
```
> **NB** Не используйте встроенную функцию `extend`, так как она не изменяет свойства исходного объекта, а создает новый.

* В **BH** в экспортируемой функции необходимо изменить глобальное свойство `bh.lib.global`:

```javascript
module.exports = function(bh) {
    bh.utils.extend(bh.lib.global, {
        id: 'auto',
        environment: 'development',
        isDebug: true,
        version: '1'
    });
};
```

<a name="bemjson"></a>
#### На этапе передачи параметров в BEMJSON

Параметры, уникальные для пользователя (например, `login`, `uid`, `user-region`), следует передавать
в поле [`params`](#fields-params) BEMJSON блока на этапе генерации страницы для конкретного пользователя.

```javascript
{
    block: 'i-global',
    params: {
        login: 'yet.another.login',
        uid: '112174243'
    }
}
```

> **NB** Для того чтобы параметры корректно передались в блок [b-page](../b-page/b-page.ru.md), блок `i-global` в
  BEMJSON-дереве должен находиться выше чем `b-page`.

<a name="get-params"></a>
### Получение значения параметров

Способы получения значения `value` для параметра `кеу`:

* В **BEMHTML** — c помощью переменной `i-global` (как и раньше): `this['i-global'].key`
* В **BH**  — параметры хранятся в библиотечной переменной `global`: `bh.lib.global.key`
* В **i-bem**  — c помощью статической функции `param`: `BEM.blocks['i-global'].param('key')`


<a name="method-makePublic"></a>
### Публичные параметры

Чтобы параметр (или набор параметров) стал доступным в JavaScript (браузере),
воспользуйтесь методом блока `makePublic(param, flag)`. <br>
Аргументы:

* `param {String|Object<String,Boolean>}` — Имя параметра или объект c именами параметров в качестве ключей и значениями `true` или `false`.
* `[flag]{Boolean}` —  Определяет доступность параметра.

**BEMHTML**

```javascript
    var glob = this['i-global'];
    glob.makePublic('param');
    glob.makePublic('param', false);
    glob.makePublic({first: true, second: false});
```

**BH**

```javascript
    var glob = bh.lib.global;
    glob.makePublic('param');
    glob.makePublic('param', false);
    glob.makePublic({first: true, second: false});
```

<a name="method-isPublic"></a>
Проверить доступность параметра или набора параметров в клиентском JavaScript можно с помощью метода блока `isPublic(param)`.<br>
Аргументы:

* `param {String|Object}` —  Имя параметра или объект c именами параметров в качестве ключей.

Возвращаемое значение: `{Boolean}`. `true` — параметр доступен , `false` — параметр недоступен.


### BEMJSON-поля блока

<a name="fields-params"></a>
#### Поле `params`

Тип: Object.<br>
Значения по умолчанию: смотри таблицу [Параметры блока](params) столбец «Значения по умолчанию».

Определяет набор глобальных параметров и их значений.

```javascript
{
    block: 'i-global',
    reset: true,
    params: {
        login: 'yet.another.login',
        uid: '112174243'
    }
}
```

<a name="fields-reset"></a>
#### Поле `reset`

Тип: Boolean. <br>
Значение по умолчанию: `true`.

Сбрасывает значения глобальных параметров, переданных блоку через поле `params`.
При этом значения параметров [по умолчанию](#params) и значения переданные при
 [инициализации шаблонизатора](#init) сохраняются.

Это позволяет устранить уязвимость, при которой неавторизованный пользователь (параметр `login` не задан) мог получить данные ранее авторизованного пользователя. Утечка данных происходила в версиях `islands-* 3.х` и ниже, так как значения глобальных параметров из поля `params` сохранялись между вызовами шаблонизатора разными пользователями.

Сохранить старое поведение блока позволит `reset: false` (**NB** Не рекомендуется использовать). Например, это может понадобится, если на странице используется более одного блока `i-global`. В этом случае `reset: false` следует выставить для всех блоков кроме первого.


Пример уязвимого кода из `priv.js`, который может привести к тому, что неавторизованный пользователь получит `uid` другого пользователя:

```javascript
return {
    block: 'i-global',
    reset: false,
    params: user
        ? {login: user.login, uid: user.uid}
        : {} // параметры login и uid останутся в i-global от предыдущего вызова шаблонизатора
}
```
