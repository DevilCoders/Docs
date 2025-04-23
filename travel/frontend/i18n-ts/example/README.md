# Example

В файле [exampleBuildTranslates](exampleBuildTranslates.ts) пример кода, для сборки заранее подготовленных [переводов в JSON](translates.example.json).

## i18n-sync

Получить переводы в файлы c помощью [i18n-sync](https://a.yandex-team.ru/arcadia/data-ui/i18n-sync).

Собрать переводы из полученных файлов

```ts
import {ITranslations, ELanguages, isLanguage} from '@yandex-data-ui/i18n-ts';
import {Loader, Config} from '@yandex-data-ui/i18n-sync';

export async function readFromFiles(): Promise<ITranslations> {
    const config = Config.load();
    const loader = Loader.fromConfig(config.data);
    const project = await loader.loadCurrent();

    const languages = project.getLanguages();
    const keySets = project.getKeysets();

    const translations: ITranslations = {keySets: {}};

    for (const keySet of keySets) {
        const keySetName = keySet.getName();

        translations.keySets[keySetName] = {name: keySetName, keys: {}};

        const keys = keySet.getKeys();

        for (const key of keys) {
            const keyName = key.getName();

            translations.keySets[keySetName].keys[keyName] = {
                name: keyName,
                translations: {},
            };

            for (const lang of languages) {
                if (isLanguage(lang)) {
                    continue;
                }

                const keyValue = key.getTranslation(lang).getValue();
                const sourceText = Array.isArray(keyValue)
                    ? keyValue[0]
                    : keyValue;

                translations.keySets[keySetName].keys[keyName].translations[
                    lang
                ] = {
                    lang,
                    text: typograf.execute(sourceText),
                    sourceText,
                };
            }
        }
    }

    return translations;
}
```
