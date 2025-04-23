# page-for-outdate-browsers

## Описание:

Пакет, позволяющий получать страницу-заглушку для устаревших браузеров.
Под капотом используется [библиотека](https://github.com/browserslist/browserslist-useragent) `browserslist-useragent`, позволяющая определить удовлетворяет ли useragent конфигу.

Формулировки и дизайн были согласованы с юристами и дизайнерами в рамках [задачи](https://st.yandex-team.ru/LEGAL-24818).

Дефолтный список браузеров:
```javascript
const SUPPORTED_BROWSERS_LIST = [
    'ff >= 50',
    'Chrome >= 50',
    'Opera >= 50',
    'Safari >= 9',
    'ie >= 11',
    'Edge >= 16',
    'Android >= 4.4',
    'ios_saf >= 9',
    'op_mob >= 51',
    'and_chr >= 50',
    'and_uc >= 11',
    'Samsung >= 5',
];

const UNSUPPORTED_BROWSERS_LIST = [
    'ff < 50',
    'Chrome < 50',
    'Opera < 50',
    'Safari < 9',
    'ie < 11',
    'Edge < 16',
    'Android < 4.4',
    'ios_saf < 9',
    'op_mob < 51',
    'and_chr < 50',
    'and_uc < 11',
    'Samsung < 5',
];
```

## Usage

```javascript
// получаем либо html-страницу в виде строки, либо undefined
const pageForOutdatedBrowser = getPageForOutdateBrowsers({
    useragent: 'test user agent',
    platform: 'desktop',
    logoUrl: 'https://logoUrl.com',
    favicons: '<link href="#" />',
    config: {
        supported: { ... },
        unsupported: { ... },
    }
});

if (pageForOutdatedBrowser) {
    return pageForOutdatedBrowser;
}
```

## API

```javascript
interface BrowserslistUseragentOptions {
    browsers?: string[];
    env?: string;
    ignorePatch?: boolean;
    ignoreMinor?: boolean;
    allowHigherVersions?: boolean;
}

interface IConfig {
    unsupported: BrowserslistUseragentOptions;
    supported: BrowserslistUseragentOptions;
    // Список браузеров и поддерживаемая версия, которые не распознаются "browserslist-useragent"
    // Например "{ "Samsung Internet":  3 }"
    minBrowserFamilyVersion: Record<string, nubmer>;
}

interface ITemplate {
    logoUrl: string;
    favicons?: string;
    yaMetrikaId?: number;
    nonce?: string;
}

interface IPageForOutdatedBrowsers extends ITemplate {
    useragent: string,
    platform: 'desktop' | 'touch';
    webviewDeviceType?: 'android' | 'ios';
    config?: IConfig,
}
```

[Список](https://github.com/browserslist/browserslist-useragent#supported-browsers) поддерживаемых для парсинга useragent браузеров

[Библиотека](https://github.com/browserslist/browserslist-useragent) `browserslist-useragent` использует [библиотеку](https://github.com/3rd-Eden/useragent) `useragent`, которой нужен `yamlparser`. В [readme.md](https://github.com/3rd-Eden/useragent/blob/master/README.md) `useragent` написано, что нужно добавлять `yamlparser` в `dependencies`.
