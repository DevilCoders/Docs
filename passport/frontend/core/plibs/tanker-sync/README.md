# tanker-sync

## CLI
```
node ./bin/tanker-sync --config=./config.js --history=./history.json --output=./ --languages=ru,en --host=tanker-api.yandex-team.ru
```

## Node
```
const TankerSync = require('../lib/tanker-sync');
const tankerSync = new TankerSync(options);
tankerSync.run();
```

### Параметры (options)
* `config` - js-файл с настройками для бандлов переводов (подробности - см. ниже)
* `history` - json-файл, в котором хранится история последних изменений переводов из Танкера (по умолчанию - пустой объект `{}`)
* `output` - директория для выгрузки переводов
* `languages` - список языков для выгрузки, указанных через запятую
* `host` - хост Танкера (по умолчанию - tanker-api.yandex-team.ru)

### Файл с настройками бандлов переводов
```
    const bundlesConfig = {
        bundleName: { // любой ключ-идентификатор бандла переводов
            exportFile: '../path/to/file.${LNG}.${FORMAT}',
            loadUrl: 'https://tanker-api.yandex-team.ru/..',
            projectName: 'passport',
            branchName: 'master',
            keySets: ['Errors', 'Frontend', ..],
            formats: ['json', 'loc'],
            options: {
                status: 'unapproved',
                'flat-keyset': '1'
            },
            languages: ['ru', 'en', ..]
            needMerge: true,
            forceLoad: true,
            afterSaveCallback: function () { return; },
        },
        anyBundleName: {
            ...
        },
        ...
    };

    module.exports = bundlesConfig;
```

`[Object] bundleName` - объект настроек; сам ключ используется для кэшировния запросов в Танкер и хранения истории выгрузки переводов.

Настройки бандла переводов (* - обязательные):
* `exportFile`* - путь и название экспортируемого файла, указанный относительно `options.output`; `${LNG}` и `${FORMAT}` используются для подстановки соответствующих значений при выгрузке нескольких языков или нескольких форматов файлов
* `loadUrl` - url, по которому будут отправляться запросы для выгрузки переводов
* `projectName` * - название проекта в Танкере
* `branchName` - название ветки проекта в Танкере (по умолчанию - master)
* `keySets` * - массив кейсетов проекта в Танкере
* `formats` * - формат, выгружаемого файла; поддерживаемые форматы - `json`, `js`, `loc`
* `options` - GET-параметры, передаваемые в `loadUrl`
* `languages` - список языков для конкретного бандла
* `needMerge` - флаг, используемый для объединения переводов, выгружаемых в json-формате
* `forceLoad` - флаг, который игнорирует проверку даты последнего изменения переводов в Танкере
* `afterSaveCallback` - callback-функция, которая вызывается после выгрузки переводов


Примечания:
> Если необходимо изменить настройку бандла, который закешировался в истории, то следует один раз запустить выгрузку с флагом `forceLoad`.

> Для форматов `js` и `loc` необходимо указывать только один кейсет. Для формата `json` есть возможность указывать несколько кейсетов при использовании флага `needMerge`.
