#static-combine

Набор утилит для подключения [static-combine-server](https://st.yandex-team.ru/YDO-9061) к сервису

##StaticCombineManifestCreatorPlugin

Плагин для сбора информации о расположении статики с присвоением уникального идентификатора для каждого файла.

Нужен для синхронизации информации о расположении статики между сервисом и static-combine-server. В запросе к static-combine-server оперируем получившимися идентификаторами.

Опции плагина для собирания информации о расположении статики:
 * filename (optional) - имя файла манифеста
 * project - название проекта, для которого генерируется файл
 * version (optional) - версия статики

Пример подключения:
```javascript
{
    plugins: [
        new StaticCombineManifestCreatorPlugin({
            project: 'ydo',
            filename: '../../static/static-combine-manifest.json',
        }),
    ]
}
```

Пример сгенерированного манифеста:
```json
{
    "project": "ydo",
    "version": "2.347.0",
    "publicPath": "//frontend-test.s3.mds.yandex.net/ydo/v2.347.0/static/",
    "assets": {
        "1": "//frontend-test.s3.mds.yandex.net/ydo/v2.347.0/static/bundle1.js",
        "2": "//frontend-test.s3.mds.yandex.net/ydo/v2.347.0/static/bundle2.js",
        ...
    },
    "assetsInverted": {
        "//frontend-test.s3.mds.yandex.net/ydo/v2.347.0/static/bundle1.js": "1",
        "//frontend-test.s3.mds.yandex.net/ydo/v2.347.0/static/bundle2.js": "2",
        ...
    }
}
```

##getCombinedStaticUrl

Функция для генерации урла до static-combine-server.
Параметры функции:
```typescript
{
    project: string; // название проекта
    type: StaticServerUrlType; // тип загружаемого ресурса (js/css)
    staticManifest: IStaticCombineManifest; // манифест из плагина StaticCombineManifestCreatorPlugin
    chunks: IStaticCombineServerChunk[]; // массив урлов чанков
    normalizeChunkIds?: boolean; // флаг для нормализации чанков, нужен для js чанков
    endpoint?: string; // ссылка до static-combine-server (default: //yastatic.net/static-combine-server)
    manifestUrl: string; // ссылка до загруженого манифеста из плагина StaticCombineManifestCreatorPlugin
}
```

Пример вызова функции:
```typescript
const combineServerUrl = getCombinedStaticUrl({
    project: env.isProduction ? 'ydo' : 'ydo-testing',
    type: StaticServerUrlType.SCRIPT,
    staticManifest,
    chunks,
    normalizeChunkIds: true,
    manifestUrl: staticCombineManifest,
    endpoint: state.experiment.flags.static_combine_server_endpoint,
})
```

Пример подключения полученного урла: `<script async src="${combineServerUrl}" crossorigin data-chunk="combined"></script>`
