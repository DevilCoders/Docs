# MBO-CORE

Пакет содержит скрипт для сборки и запуска проектов MBO, инкапсулируя в себе всю инфраструктурную часть

### Подключить к своему проекту

1. Устанавливаем пакет @yandex-market/mbo-core:

```bash
npm install @yandex-market/mbo-core --save-dev
```

2. Добавить команды запуска и сборки в package.json

```
...
"scripts: {
  "start": "mbocore start"
  "build": "mbocore build"
  "test": "mbocore test"
  "test:coverage": "mbocore test --coverage"
}"
...
```

Команда test принимает те же аргументы, что и jest

3. (Необязательно) Добавить конфиг .mbocore.config.js

```
module.exports = {
  tsconfig: 'path/to/your/tsconfig.json',
  htmlTemplate: 'path/to/index.html',
  host: 'localhost.msup.yandex-team.ru',
  port: 8449,
  ssl: {
    keyFile: path/to/your/yandex-team.key,
    crtFile: path/to/your/yandex-team.crt,
  };
  bundleAnalyzer: true,
  apiDist: [
    {
        path: '/api',
        target: 'https://best-service.yandex-team.ru',
        secure: false,
        changeOrigin: true,
        cookie: 'highlander=Duncan',
    }
  ],
  webpack: (config) => {
    return {...config, target: 'es5'};
  }
  webpackDevServer: (config) => {
    return {...config, host: 'my-host.ru'};
  },
  testConfig: {
    // jest конфигурация, которая смерджится с конфигом по умолчанию
    // Но есть один момент:
    // если в поле moduleNameMapper для какого-то ключа указано true,
    // то подставится [identity-obj-proxy](https://www.npmjs.com/package/identity-obj-proxy)
    moduleNameMapper: {
      '\\.(css|less|scss|sass)$': true,
    },
    coverageThreshold: {
      global: {
        lines: 99,
      },
    },
  }
};
```

### Создать новый проект

1. Устанавливаем пакет @yandex-market/mbo-core:

```bash
npm install -g @yandex-market/mbo-core
```

2. Генерируем новый проект:

```bash
mbocore new --name my-app --description "Это будет в package.json"
```

### Разработка пакета mbo-core

1. Устанавливаем зависимости:

```bash
npm ci
```

2. Создаём связь на проект, где используется mbo-core

В папке mbo-core

```bash
npm link
```

В папке проекта

```bash
npm link @yandex-market/mbo-core
```

3. Запускаем сборку с флагом watch

```bash
npm run start
```

4. В своём проекте пробуем одну из команд

```bash
mbocore start
```
