## ServerManifestExtras
Добавляет к результату [ServerManifestPlugin](../../../../ps-build/lib/webpack/plugins/ServerManifestPlugin) секцию с информацией про языковые бандлы.

### Extras
#### manifest.json
Добавлена секция внутрь entry с информацией о стартовых языковых ассетах.<br>
Асинхронных языковых ассетов в списке нет.
```json
{
  "entries": {
    "<entry name>": {
      ...
      "langs": {
        "ru": [
          "asset-1.ru.js"
        ],
        "en": [
          "asset-1.en.js"
        ]
      }
    }
  }
}
```

#### manifest.js
Добавлен новый метод `getFilesByLang`.

В отличии от базового метода манифеста [getFiles](../../../../ps-build/lib/webpack/plugins/ServerManifestPlugin#getfiles-entryname-string--string)
##### getFilesByLang( entryName: string, land: string ): string[]
Возвращает список файлов, необходимых для полноценной работы entry.
Отфильтровывает из финального списка языковые ассеты не относящиеся к указанному языку.
