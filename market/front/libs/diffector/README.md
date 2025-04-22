# diffector

Анализ связей в проекте и их изменений

![](screencast.gif)

- [Usage](#usage)
- [Настройка локального окружения для отправки отчетов в Трекер](#настройка-локального-окружения-для-отправки-отчетов-в-трекер)
- [Configure](#configure)
- [Reporters](#reporters)

## Usage

```bash
$ diffector -h
Usage: diffector [options]

Options:
  --version             Show version number                            [boolean]
  --config, -c          The path to a diffector config file.            [string]
  --sources                                                              [array]
  --baseBranch, -b                                                      [string]
  --compareBranch, -f                                                   [string]
  --interactive, -i                                                    [boolean]
  --verbose, -v                                                        [boolean]
  --matchPatterns                                                        [array]
  --debug                                                              [boolean]
  --selectBranches, -s                                                 [boolean]
  --reporters                                                            [array]
  -h, --help            Show help                                      [boolean]
```

## Настройка локального окружения для отправки отчетов в Трекер

Для работы с [API Стартрека](https://wiki.yandex-team.ru/tracker/api/) локально,
создайте в корне проекта файл `.env` и укажите в нем переменную окружения `ST_OAUTH_TOKEN`
как в [.env.example](./.env.example). [**Получить токен можно тут**](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b)

> Не забудьте добавить `.env` в `.gitignore`!

## Configure

Основные опции и значения по умолчанию:

- [type BaseOptions](src/deps-diff/args.ts#L49) - общие опции
- [type ConfigOptions](src/deps-diff/args.ts#L77) - опции конфига
- [defaults](src/deps-diff/args.ts#L103) - опции по умолчанию

Для начала работы в корне проекта создайте `diffector.config.js`:

```js

// для быстродействия нужно предварительно отпарсить tsConfig
const ts = require('typescript');
const tsParsedConfig = ts.readJsonConfigFile('./tsconfig.json', ts.sys.readFile);
const {raw: tsConfig} = ts.parseJsonSourceFileConfigFileContent(tsParsedConfig, ts.sys, '.');

module.exports = {
  // По умолчанию сначала смотрим есть ли локальный мастер, если есть сравниваем с ним,
  // если нет, то проверяем есть ли origin/master
  baseBranch: ['master', 'origin/master'],
  // так же можно указать просто строку, но тут надо учитывать, что в окружении CI, как и в локальном
  // эта ветка тоже должна быть, а локально бывает удобнее сравнивать с мастером
  // baseBranch: 'origin/master',
  tracker: {
    // Очередь используется для отправки отчета в тикет,
    // номер тикета парсится из ветки вида feature/1234-branch (RegExp: `/\d+/`)
    queue: 'VNDFRONT',
  },
  // Returns "1" match from pattern or null
  // matchPatterns is syntax sugar for "match" function (it used for generating "match" function)
  matchPatterns: [
    /src\/pages\/(.*?)\//,
    /src\/pages\/(.*?)\.js/,
    /app\/pages\/\w+\/(.*?)\//,
    /app\/pages\/\w+\/(.*?)\.js/,
  ],
  // Регулярные выражения для преобразование имени файла, по какому либо правилу
  mapByPatterns: [/app\/resource\/((?!mbiPartner).[^/]*)/g],
  // Same as matchPatterns, returns name of page
  // match function will override matchPatterns
  match: filepath =>
    (filepath.match(/src\/pages\/(.*?)\//) ||
      filepath.match(/app\/pages\/\w+\/(.*?)\//) ||
      filepath.match(/src\/pages\/(.*?)\.js/) ||
      filepath.match(/app\/pages\/\w+\/(.*?)\.js/) ||
      [])[1],
  // Файлы проекта по которым отслеживать изменения
  sources: ['./src/**/*.{js,jsx}'], 
  // конфиг для библиотеки dependency-tree https://github.com/dependents/node-dependency-tree
  // достаточно указать webpack и tsConfig
  dependencyTreeConfig: {
    webpackConfig: './configs/webpack/webpack.config.client.js',
    tsConfig,
  },
  // Функции по кастомной связке зависимостей в проекте
  resolver: [myCustomResolver],
  // Default reporters
  reporters: [
    'pages', // Выводит с затронутых страниц
    'libs', // Выводит список измененных внешних зависимостей
    'tracker', // Отправляет в Трекер отчет со страницами и зависимостями
    'summary', // Выводит общее кол-во затронутых страниц
  ],
  // Точки входа, страницы или модули
  entries: {
    Analytics: 'src/pages/Analytics',
    AnalyticsReport: 'src/pages/Report',
    ModelsPromotion: ['src/pages/ModelsPromotion', 'src/api/ModelsPromotion'],
  },
  // Будут выводиться рядом с названием страницы
  aliases: {
    '[id]/promotion/models': 'ModelsPromotion',
  },
}
```

## Reporters

[type ReporterOptions](src/deps-diff/args.ts#L15) - данные которые приходят в reporter

```js
// diffector.config.js

const { formatList } = require('diffector/format')

const exampleReporter = async ({ result }: ReporterOptions) => {
  console.log(formatList(result))
}

module.exports = {
  reporters: [
    // Используем один из дефолтных репортеров + кастомный
    'tracker',
    exampleReporter,
  ],
}
```

## Resolvers

Данное API предоставляет возоможность производить кастомную связку зависимостей.

- `run` - функция выполняющая итерацию и возврат зависимостей, которые нужно слинковать с файлом.
- `options` - объект типа [ResolverOptions](src/deps-diff/resolver.d.ts#L3). По умолчанию принимает параметр [resolve](src/deps-diff/args.ts#L83), переданный в конфигурацию `diffector`

### Example

```js
// diffector.config.js

const apiResolverRunner = (files, options) => {
  // тут может происходить какая внутренняя логика по поиску файлов в проекте
  const apiMap = getApiMap(apiPageRoutes, options)

  // раннер возвращает функцию-итератор, которая будет возвращать путь к зависимости при каждом сопоствлении строки в файле
  function* dependencyIterator(file, content) {
    let matched

    while ((matched = /api:(.?)*[a-z]/gi.exec(content))) {
      const [apiName] = matched

      if (apiName && apiMap[apiName]) {
        yield apiMap[apiName].path
      }
    }
  }

  return dependencyIterator
}

const apiResolver = {
  run: apiResolverRunner,
  options: {
    skip: /\.spec\.js$/,
  },
}

module.exports = {
  resolvers: [apiResolver],
}
```

# TODO

- [ ] Сделать resolveThrowActions
- [ ] Подумать над настраиваемыми стратегиями резолвига (как resolveThrowActions)
- [ ] Собрать args, run и prompt в `src/cli/`
- [ ] `diffector master`, `diffector master..HEAD^`
- [ ] Сортировка итогового списка страниц по алфавиту
- [ ] Объединение страниц по изменениям
      (Если у страниц одинаковый набор изменений, то они объединяются)
- [ ] Группировка страниц по папке (но тогда нужно в регулярках матчится на `/app\/(resource\/\w+\/.*?)$/` )
      и потом как-то отдельно еще доставать название страницы, а может **path-to-regexp**

## TODO (release-checker)

Можно сделать так

- запускаешь тулзу
- она проверяет релиз
- если все ок предлагает создать
- переводит тикеты в нужный статус
