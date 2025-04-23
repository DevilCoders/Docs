# ServerManifest Plugin
- [Настройки](#Настройки)
- [Использование](#Использование)
- [Manifest Json](#Manifest-json)
- [Manifest Runtime](#Manifest-runtime)
- [Build Hooks](#Build-hooks)

Генерирует специальный манифест из двух файлов [Manifest Runtime](#Manifest-runtime) и [Manifest Json](#Manifest-json).

Помогает удобно работать с результатами сборки на сервере.

### Настройки
- **name** (default: 'manifest') - базовая часть имени манифеста.<br>
Может быть абсолютным или относительным (относительно output.path) путем<br>
Не надо добавлять к имени расширение `js` или `json` - плагин сделает это сам.

- **manifestName** (default: '[name].json') - путь до сгенерированного [json](#Manifest-json) файла.<br>
В шаблоне может участвовать базовая часть имени из пареметра `name`. (Пример в `default`)

- **runtimeName**  (default: '[name].js') - путь до сгенерированного [runtime](#Manifest-runtime) файла.<br>
В шаблоне может участвовать базовая часть имени из пареметра `name`. (Пример в `default`)

- **watchJson** (default: false) - добавляет в [runtime](#Manifest-runtime) секцию для фонового обновления [json](#Manifest-json) файла.<br>
Не рекомендуется использовать в проде.

- **resolveModules** (default: false) - добавляет в [runtime](#Manifest-runtime) поле `modules` и заполняет его собранными commonjs модулями.<br>
Актуально для серверной сборки. В дальнейшем можно использовать с кастомным webpack рантаймом.

- **omitRuntimeFiles** (default: false) - убирает из [json](#Manifest-json) ссылки на сгенерированный webpack рантайм.<br>
На сервере сгенерированный рантайм бесполезен. Если включен `resolveModules`, то этот рантайм загрузится в modules, но никак не будет использован.<br>
`omitRuntimeFiles` избавляет от подобного поведения.

### Использование
```js
const manifest = require('./artifacts/manifest');
const entryName = 'main';

console.log(manifest.getFiles(entryName));
```

### Manifest Json
Один из генерируемых на выходе файлов.<br>
По умолчанию складывается в сборочную директорию в `manifest.json`.<br>
Имя и расположение настраиваются с помощью опций `name` и `manifestName`.

Использовать напрямую не стоит, лучше брать фасад в виде [runtime](#Manifest-runtime).
Но знать о существовании важно, чтобы не забыть положить в пакет с приложением.

### Manifest Runtime
Один из генерируемых на выходе файлов.<br>
По умолчанию складывается в сборочную директорию в `manifest.js`.<br>
Имя и расположение настраиваются с помощью опций `name` и `runtimeName`.

#### Публичное API
Набор методов может быть расширен через сборочный хук `runtimeMethods`.

##### **publicPath**: string
Путь на CDN относительно которого резолвятся все файлы (без uri схемы).

##### **publicHost**: string
CDN хост, на котором находятся все файлы (без uri схемы).

##### **filePath( fileName**: string **)**: string
Возвращает абсолютный путь до файла на CDN.

##### **getEntry( entryName**: string **)**: Entry
Возвращает весь объек Entry.
```ts
interface Entry {
    entryModule: string | number,
    files: string[]
}
```
Содержимое Entry может быть модифицировано через сборочный хук `entryResolved`.

##### **getFiles( entryName**: string **)**: string[]
Возвращает список файлов, необходимых для полноценной работы entry.

##### **getEntryModule( entryName**: string **)**: string|number
Возвращает id модуля необходимого для запуска работы entry.

### Build Hooks
Доступ к хукам через `getCompilerHooks`:
```js
const { ServerManifestPlugin } = require('@ps-int/ps-build');

class SomeExternalPlugin {
    apply(compiler) {
        const hooks = ServerManifestPlugin.getCompilerHooks(compiler)
    }
}
```

- **entryResolved( entryInfo**: Entry **, entry**: Webpack.ChunkGroup **)**: [Entry](#getEntry)<br>
Триггерится на каждый найденный и удачно собранный entry.

- **runtimeMethods( methods**: string **)**: string<br>
Триггерится в момент генерации рантайма, позволяет расширить набор методов.

- **beforeEmitManifest( manifest**: json **)**: json<br>
Триггерится после генерации манифеста, позволяет расширить набор полей.
 
- **beforeEmitRuntime( runtime**: string **)**: string<br>
Триггерится после генерации рантайма, позволяет дописать в модуль новую логику.
