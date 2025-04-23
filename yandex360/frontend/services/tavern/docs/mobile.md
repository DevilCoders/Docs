#### Переменные шаблона

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
JSON представление интерфейса [SessionConfig](../client/entries/mobile/types.ts);



###### `{{ENVIRONMENT_CONFIG}}`
JSON представление интерфейса [EnvironmentConfig](../client/entries/mobile/types.ts);

#### Манифест
JSON-файл с описанием как открывать вебвью и как обновлять статику.

Настраивается в [конфиге вебпака](../client/webpack/webpack.mobile.extras.js)

#### События 

|name|payload|
|-|-|
|`setTheme`|см. [MobileTheme](../client/entries/mobile/types.ts)|
|`setServicesNotifications`|см. [SessionConfig.servicesNotifications](../client/entries/mobile/types.ts)|
