# tap-lighthouse-ci

Пакет для запуска Lighthouse CI в проектах [TAP](https://abc.yandex-team.ru/services/turboappplatform/).

## Установка

Для установки пакета следует выполнить в корне репозитория:

```bash
npx lerna add @yandex-int/tap-lighthouse-ci --scope=<package-name>
```

где `<package-name>` - название пакета, куда нужно установить `tap-lighthouse-ci`.

## Конфигурация

1. Добавляем скрипт в `package.json` сервиса:

    ```
    "scripts": {
        "ci:pulse:shooter": "(if [[ \"$PLATFORM\" == \"touch\" ]]; then npm run ci:build && tap-lighthouse-ci ; fi) >& __reports/lighthouse.log"
    }
    ```

2. Создаем проект на LHCI сервере через
 
    ```
    NODE_TLS_REJECT_UNAUTHORIZED='0' npx @lhci/cli wizard
    > Which wizard do you want to run? new-project
    > What is the URL of your LHCI server? https://lhci.tap-tst.yandex.ru/
    > What would you like to name the project? <project_name>
    > Where is the project's code hosted? https://github.yandex-team.ru/search-interfaces/frontend
   ```
    
в результате получаем токен.

3. Добавляем конфиг в `<service>/.config/lighthouse-config.json`. Пример:

    ```json
    {
        "ci": {
            "collect": {
                "url": ["http://localhost:5000/pogoda/", "http://localhost:5000/pogoda/details/tomorrow"],
                "numberOfRuns": 3,
                "startServerCommand": "npx serve -c ./.config/serve.json -s build",
                "startServerReadyPattern": "Accepting connections",
                "settings": {
                    "chromeFlags": "--no-sandbox"
                }
            },
            "upload": {
                "serverBaseUrl": "https://lhci.tap-tst.yandex.ru/",
                "token": "{TOKEN}"
            }
        }
    }
    ```

4. Добавялем конфиг для пакета `serve` (опционально). Пример:
    ```json
    {
        "headers": [
            {
                "source": "**/*",
                "headers": [
                    {
                        "key": "Cache-Control",
                        "value": "public, max-age=3600000"
                    }
                ]
            }
        ]
    }
    ```

## Релиз новой версии докер-образа

Для выпуска новой версии образа нужно:

1. Поправить версию в файле `docker/build.sh`
2. Поправить версию в файле `docker/Dockerfile`
3. Собрать и залить в registry новый образ: `(cd docker && ./build.sh)`
