Генерирует `manifest.json` согласно [документации](https://wiki.yandex-team.ru/yandexmobile/browser/tz/Platforma-dlja-WebAPPov/AppDocumentation/#realizacijaivykladkamanifesta)
На вход нужно передать файл конфигурации.

### Пример
`node generate-manifest.js --config=./config/manifest.config.js`

В конфиге можно указать:
- манифест по [спеке](https://developer.mozilla.org/ru/docs/Mozilla/Add-ons/WebExtensions/manifest.json)
- поле `yandexManifest` (нужно для турбоаппа и кеширования с помощью сервис воркера)
- `buildDir` - массив путей до локальной статики для кеширования
- `outputDir` - путь, куда положить файл с манифестом
- `staticFiles` - непосредственно урлы статики

Пример файла конфига [тут](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/news/.config/manifest.js)
