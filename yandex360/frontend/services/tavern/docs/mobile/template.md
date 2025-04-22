## Шаблон

Представляет собой html-файл с переменными шаблона, которые будут заменены на реальные значения перед открытием в вебвью.

### Переменные шаблона

###### `{{LOCALE}}`
язык ```ru,en```, всего МЯП поддерживает 4 языка.
'ru', 'en', 'tr', 'uk'

###### `{{NONCE}}`
случайная строка
Пример с swift
```swift
let uuid = {
    var bytes = [UInt8](repeating: 0, count: 16)
    _ = SecRandomCopyBytes(kSecRandomDefault, bytes.count, &bytes)
    return Data(bytes).base64EncodedString()
}()
```

###### `{{CONNECTION_ID}}`
Используется для логирования 

###### `{{VIEWPORT_SCALE}}`
В 99% случаев
```
width=device-width,initial-scale=1,user-scalable=no,minimum-scale=1,maximum-scale=1
```

###### `{{TLD}}`
```ru, com```

###### `{{SESSION_CONFIG}}`
JSON представление интерфейса [SessionConfig](../../client/entries/mobile/types.ts);


###### `{{ENVIRONMENT_CONFIG}}`
JSON представление интерфейса [EnvironmentConfig](../../client/entries/mobile/types.ts);

Подставляется в html tag script
```html
<script id="session-config" charset="utf8" type="application/json" nonce="${NONCE}">${SESSION_CONFIG}</script>
```

Затем парсится в js точке входа

```js
const sessionConfigNode = document.querySelector('#session-config');
const sessionConfig = JSON.parse(sessionConfigNode.textContent);
```

####{{ENVIRONMENT_CONFIG}}
JSON представление интерфейса [EnvironmentConfig](../../client/entries/mobile/types.ts);

Подставляется в html tag script
```html
<script id="environment-config" charset="utf8" type="application/json" nonce="${NONCE}">${SESSION_CONFIG}</script>
```

Затем парсится в js точке входа

```js
const environmentConfigNode = document.querySelector('#environment-config');
const environmentConfig = JSON.parse(environmentConfigNode.textContent);
```

### Манифест
JSON-файл с описанием как открывать вебвью и как обновлять статику.

Настраивается в [конфиге вебпака](../../client/webpack/webpack.mobile.extras.js)
