# Конфиг

## Формат конфига
Конфиг может примимать следующие параметры:
* `testMatch` - [string[]] Массив строк с паттернами для поиска файлов тестов.
* `reportPath` - [string] Путь к файлу отчета о статусе тестов.
* `staticMocks` - [object[]] Конфигурация для записи и воспроизведени статических моков.
* `dynamicMocks` - [object[]] Конфигурация для записи и воспроизведения динамических моков.
* `matchImageSnapshotOptions` - [object] Конфигурация для сравнения скриншотов.
* `timeout` - [object] Jest таймаут. Задает через какое время считать тест не пройденным.

## Стандартный конфиг
Стандартный конфиг выглядит следующим образом:
```ts
const defaultConfig: Required<Config> = {
    testMatch: ['./tests/**/*.test.ts?(x)'],
    reportPath: './reports/index.html',
    staticMocks: [],
    dynamicMocks: [
        {
            match: (req): boolean => req.url().includes('/api/'),
            buildKey: (req): string => {
                const reqUrl = req.url();
                const postData = req.postData();
                const body = postData ? {...JSON.parse(postData), csrfToken: undefined} : postData;
                const parsedUrl = new url.URL(reqUrl);

                return `${parsedUrl.pathname}${parsedUrl.search}${JSON.stringify(body)}`;
            }
        }
    ],
    matchImageSnapshotOptions: {
        failureThreshold: 0.00001,
        failureThresholdType: 'percent'
    },
    timeout: 30000
};
```
Если он вам подходит, то дополнительно ничего создавать не нужно.
#### Примечание: pup попытается смержить стандартный конфиг с вашим.

## Генерация конфига
Чтобы сгенерировать стандартный конфиг исполните команду:
```
npx pup init
```
После выполнения конфиг будет доступен по пути `./pup.config.ts`. Так же будет создан демонстрационный тест(`./tests/demo.test.ts`).
