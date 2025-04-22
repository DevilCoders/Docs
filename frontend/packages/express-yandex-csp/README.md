# express-yandex-csp
Мидлвара для генерации заголовка Content-Security-Policy. Создана на основе [express-csp-header](https://github.com/frux/csp/blob/master/packages/express-csp-header/).

## Умеет
 * автоматически генерировать ключ [nonce](#nonce)
 * расширять политики с помощью пресетов
 * вшит дефолтный адрес report-uri в соотвествие с [рекомендациями](https://wiki.yandex-team.ru/product-security/csp/#prijomotchetovonarushenijax) отдела СИБ
 * поддерживает новый способ отправки отчетов о нарушении [report-to](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/report-to)

[Общие рекомендации СИБ для CSP](https://wiki.yandex-team.ru/product-security/csp)

## Использование
```js
const { expressYandexCsp } = require('express-yandex-csp');

app.use(expressYandexCsp(params));
```

`params` – объект, содержащий следующие параметры:
- `directives` – директивы CSP. Единственная обязательная опция;

- `presets` – пресеты правил. [Подробнее](https://github.yandex-team.ru/project-stub/express-yandex-csp#Пресеты-список);

- `reportUri` – адрес для отсылки отчетов о нарушении политики. [Устаревший](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/report-uri) способ. Используется для обратной совместимости со старыми браузерами. [Подробнее](#report-uri);
- `reportTo` – описание груп эндпоинтов для отправки отчетов о нарушениях [Подробнее](#report-uri);

- `useDefaultReportUri` – флаг использования адреса для отчетов, [рекомендованного](https://wiki.yandex-team.ru/product-security/csp/#prijomotchetovonarushenijax) отделом СИБ. При установке в `true` отменяет предыдущий параметр;

- `from` – используется при анализе поступающих отчетов о нарушениях CSP для группировки по различным сервисам Яндекса. Может содержать любую необходимую информация для идентификации политики или интерфейса, к примеру: `morda.touch.ru`;

- `project` – используется при анализе поступающих отчетов о нарушениях CSP для группировки по различным сервисам Яндекса. Это должно быть название на английском языке (URL текущей страницы использовать нельзя) и едино для всего сервиса, к примеру `morda`;

- `domainOptions` – опции парсинга TLD для автоматической подстановки в правила. [Подробнее](#поддержка-кастомных-не-icann-tld);

- `reportOnly` - отправлять заголовок `Content-Security-Policy-Report-Only` вместо `Content-Security-Policy` (не блокирует запросы, а только отсылает отчет о нарушениях)

## Использование c дефолтными политиками
Дефолтные политики убраны с версии `4.0.0`.

## Формат правил политики
Правила политика безопасности – это объект вида "ключ: массив строк", содержащий правила. Например:
```js
{
    directives: {
        'default-src': ["'none'"],
        'script-src': ["'self'", 'yastatic.net'],
        'style-src': ["'self'", "'unsafe-inline'", 'yastatic.net'],
    },
}
```

## Адрес отсылки отчетов о нарушении CSP
Может быть указан тремя способами.

**Важно**: если вы не используете дефолтный адрес для отправки отчетов, то имейте в виду, что директива `report-uri` на данный момент [устарела](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/report-uri) и должна быть продублирована новой директивой `report-to` и заголовком `Report-To` ([подробнее](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/report-to)). Пример можно найти ниже.

#### Первый. Дефолтный.
Преимущества дефолтного урла:
  - он [рекомендован](https://wiki.yandex-team.ru/product-security/csp/#prijomotchetovonarushenijax) СИБ
  - логи нарушений можно посмотреть на [https://csp.yandex-team.ru](https://csp.yandex-team.ru/)
  - нет необходимости отдельно указывать директиву `report-to` и заголовок `Report-To`. [Подробнее](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/report-to)

**Важно**: в отчет включается логин и uid пользователя, нарушевшего CSP. Они берутся из `req.cookie`. Поэтому `express-yandex-csp` нужно подключать **после** парсера кук.

Чтобы воспользовать преднастроенным адресом указываем название вашего сервиса `project`, в `from` пишем идентификатор и ставим `useDefaultReportUri` в `true`:
```js
app.use(cookieParser());
app.use(expressYandexCsp({
    directives: directives,
    useDefaultReportUri: true,
    project: 'my-super-service',
    from: 'ru.touch.my-super-service',
}));
```

#### Второй. Статичный.
Если у вас есть свой адрес для сбора отчетов и адрес у него всегда статичный, то просто передайте этот адрес в параметре `reportUri`.
```js
app.use(expressYandexCsp({
    directives: {
      'report-to': 'my-report-group',
    },
    reportUri: 'https://cspreport.com/send',
    reportTo: [
        {
            group: 'my-report-group',
            max_age: 30 * 60,
            endpoints: [{ url: 'https://cspreport.com/send'}],
            include_subdomains: true
        }
   ],
}));
```

#### Третий. Динамический.
Если ваш адрес для отчетов динамический (например, необходимо передавать какие-то параметры), то передайте в параметре `reportUri` и `reportTo` функцию, которая вернет адрес:
```js
app.use(expressYandexCsp({
    directives: {
      'report-to': 'my-report-group',
    },
    reportUri: (req, res) => `https://cspreport.com/send?user=${req.userLogin}`
    reportTo: [
        {
            group: 'my-report-group',
            max_age: 30 * 60,
            endpoints: (req, res) => [{ url: `https://cspreport.com/send?user=${req.userLogin}`}],
            include_subdomains: true
        }
   ],
}));
```

## nonce
Модуль умеет автоматически генерировать ключ `nonce` для инлайновых скриптов и стилей. Для того, чтобы его использовать просто укажите ключевое слово `%nonce%`. При каждом запросе оно будет заменено на случайно сгенерированный ключ. Сгенерированый ключ будет храниться в `req.nonce`, чтобы вы его потом могли указать в атрибуте тега:
```js
app.use(expressYandexCsp({
    directives: {
        'script-src': ['%nonce%']
    }
}));
// заголовок будет иметь вид "Content-Security-Policy: scirpt-src 'nonce-Z9iP034EIZBkMe2JDAwRVw==';"

app.use(function(req, res, next) {
    console.log(req.nonce); // 'Z9iP034EIZBkMe2JDAwRVw=='
});
```

### Пресеты ([список](#Список-доступных-пресетов))
* [csp-presets-pack](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/csp-presets-pack) — пакет с набором пресетов для самых разных сервисов Яндекса и не только

Про то, как использовать и писать свои пресеты можно прочитать [в документации `csp-header`](https://github.com/frux/csp/tree/master/packages/csp-header).

## Content-Security-Policy-Report-Only
Для использования режима Report-Only нужно указать параметр reportOnly:
```js
app.use(expressYandexCsp({
    directives: {
        'script-src': ['mystatic.com']
    },
    reportOnly: true
}));
```

## Автоматическая подстановка tld
Если вам необходимо подставлять в правило текущий tld, то просто замените его ключевым словом `%tld%`:
```js
app.use(expressYandexCsp({
    directives: {
        'script-src': ['mystatic.%tld%']
    }
}));
/* для хоста myhost.com заголовок будет иметь вид "Content-Security-Policy: scirpt-src mystatic.com;"
   а для хоста myhost.net "Content-Security-Policy: scirpt-src mystatic.net;" */
```

### Поддержка кастомных (не ICANN) TLD
По умолчанию поддерживаются все ICANN домены, а также кастомные (не ICANN) TLD Яндекса: `com.am` и `com.tc` в соответствие со страницей на [Вики](https://wiki.yandex-team.ru/LegalDep/domain/ccTLD/). Определением текущего TLD занимается [parse-domain](https://github.com/peerigon/parse-domain). При необходимости можно передать [опции этой библиотеки]((https://github.com/peerigon/parse-domain#parsedomainurl-string-options-parseoptions-parseddomainnull)) в параметре `domainOptions`.

```js
app.use(expressYandexCsp({
    directives: {
        'script-src': [`mystatic.${csp.TLD}`]
    },
    domainOptions: {
        customTlds: ['example.com']
    }
}));
// Для хоста myhost.com отправит: "Content-Security-Policy: script-src mystatic.com;"
// Для хоста myhost.example.com отправит: "Content-Security-Policy: script-src mystatic.example.com;"
```

## Release notes

#### v4.0.0
  * переписано на TypeScript
  * дефолтный экспорт заменен на именованный
  * удалены дефолтные политики
  * параметр `serviceName` переименован в `from`
  * параметр `policies` переименован в `directives`
  * минимальная версия NodeJS увеличена до 12 (ES2019)
  * добавлена поддержка [`report-to`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/report-to)

#### v3.2.0
 * Добавлена поддержка передачи опциий в [parse-domain](https://github.com/peerigon/parse-domain)
 * Добавлена поддержка по умолчанию кастомных доменов Яндекса `com.am` и `com.tc`

#### v3.1.0
 * Поддержка указания пресетов в виде объекта

#### v3.0.0
 * Node >= 4
 * Добавлена поддержка [пресетов](https://github.com/frux/csp-header#presets)

#### v2.2.0
 * Добавлена поддержка директив CSP3
 * Добавлена поддержка директив без значения (булевых директив). Например `'block-all-mixed-content': true`.

#### v2.1.1
 * Исправлена ошибка дефолтного report-uri "The header content contains invalid characters"

#### v2.1.0
 * Расширение политик

#### v2.0.0
 * Изменена политика безопасности по умолчанию [ONLINEMEDIA-122](https://st.yandex-team.ru/ONLINEMEDIA-122)

#### v1.2.0
 * Добавлен режим Report-Only

#### v1.1.0
 * Автоматическая подставновка tld (спасибо [@m-smirnov](https://github.yandex-team.ru/m-smirnov))

#### v1.0.0
 * Все три аргумента теперь передаются одним объектом
 * В дефолтной политике правило data: перенесено из секции default-src в img-src
