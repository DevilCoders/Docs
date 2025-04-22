# hermione-ya-commands

Плагин для hermione, содержащий набор общих кастомных команд для использования в разных проектах.

## Установка
Плагин доступен через npm.
```
npm i -D @yandex-int/hermione-ya-commands --registry=http://npm.yandex-team.ru
```

## Конфигурация
Для включения плагина нужно указать его в конфиге hermione и выставить `enabled: true`:
```js
// В файле конфигурации hermione
module.exports = {
    plugins: {
        '@yandex-int/hermione-ya-commands': {
            enabled: true,
            commandDuplicationWarning: true,
        },
        // ...
    },
};
```

Если в проекте есть одноимённые команды, то они будут иметь больший приоритет чем команды из плагина, при этом будет выводиться предупреждение о дублировании. Его можно выключить убрав из конфига опцию `commandDuplicationWarning`.

## API команд

### `yaAssertElementsCount(selector: string, count: number, message: string): Promise<void>`
Проверяет, что число элементов равно ожидаемому.

### `yaAssertURL(actualUrl: string, expectedUrl: TExpectedUrl, message?: string, params?: TParams): Promise<void>`
Проверяет, что actualUrl соответствует expectedUrl.
```ts
type TExpectedUrl = string | { url?: string; queryValidator?: Function };

type TParams = {
    skipProtocol?: boolean;
    skipHostname?:boolean;
    skipPathname?: boolean;
    skipQuery?: boolean;
    skipHash?: boolean;
}
```
### `yaClickAtTheMiddle(selector: string):  Promise<void>`
Клик в центр элемента

### `yaOpenPageByUrl(url: string | URLLike, selectors?: string | string[]): Promise<void>`
Открывает указанный url. url может быть строкой или объектом, соответствующим [node модулю `url`](https://nodejs.org/docs/latest-v12.x/api/url.html#url_url):
```ts
type URLLike = Partial<{
    hash: string;
    host: string;
    hostname: string;
    href: string;
    password: string;
    pathname: string;
    port: string;
    protocol: string;
    search: string | Record<string, string>;
    username: string;
}>;
```
В качестве базового URL берется значение `baseUrl` из конфига hermione.

Если переданы `selectors`, то после загрузки страницы при помощи команды `yaShouldSomeBeVisible` проверяется видимость элементов с указанными селекторами.

### `yaScroll(value: string | number):  Promise<void>`
Скролит к нужному элементу либо на определённое количество пикселей.

### `yaShouldBeVisible(selector: string, message?: string):  Promise<void>`
Проверяет, что элемент видим в данный момент. Если по селектору выберется несколько элементов, выбросит ошибку.

### `yaShouldBeVisibleWithinViewport(selector: string, message?: string):  Promise<void>`
Проверяет, что элемент видим и находится в пределах вьюпорта. Если по селектору выберется несколько элементов, выбросит ошибку.

### `yaShouldExist(selector: string, message?: string):  Promise<void>`
Проверяет, что элемент существует на странице в данный момент.

### `yaShouldNotBeVisible(selector: string, message?: string):  Promise<void>`
Проверяет, что элемент невидим/отсутствует в данный момент. Если по селектору выберется несколько элементов, выбросит ошибку.

### `yaShouldNotExist(selector: string, message?: string):  Promise<void>`
Проверяет, что элемент не существует на странице в данный момент.

### `yaShouldSomeBeVisible(selector: string,  message?: string): Promise<void>`
Проверяет, что хотя бы один элемент с указанным селектором виден.

### `yaVisibleCount(selector: string,  message?: string): Promise<number>`
Возваращает количество видимых элементов по переданному селектору.

### `yaWaitForHidden(selector: string, timeout?: number | string, message?: string): Promise<void>`
Обёртка над стандартной командой waitForVisible. Позволяет указывать произвольное сообщение об ошибке.

### `yaWaitForPageLoad(): Promise<void>`
Дожидается загрузки страницы, либо падает с ошибкой, если страница не загрузилась в течение 30 секунд.

### `yaWaitForVisible(selector: string, timeout?: number | string, message?: string, reverse: boolean = false): Promise<boolean>`
Обёртка над стандартной командой waitForVisible. Позволяет указывать произвольное сообщение об ошибке.

[sd]: https://nodejs.org/docs/latest-v12.x/api/url.html#url_url
