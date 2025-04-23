# @yandex-int/package-checker

Линтер пакетов для фронтенд-монореп. Используется для унифицированной конфигурации и запуска пакетных проверок.

## Использование

CLI:

```
npx @yandex-int/package-checker --root=path --config=path --fix

Options:
  --help     Show help                    [boolean]
  --root     Monorepo root path           [string] [default: .]
  --config   package-checker config path  [string] [default: .config/package-checker.js]
  --fix      apply fixes                  [boolean][default: false]
```

API:

```typescript
import { PackageChecker } from "@yandex-int/package-checker";

// Вторым аргументом опционально можно передать конфиг.
const checker = new PackageChecker(process.cwd());
const errors = await checker.check();

// Применить фиксы, если возможно.
await checker.check({ fix: true });
```

## Конфигурация

### Правила

По умолчанию ни одно из правил не включено. Включать нужно в конфиге – `.config/package-checker.js`.

Пример:

```javascript
const npmPackageJsonLintConfig = require('./npm-package-json-lint');

module.exports = {
    rules: {
        "is-typescript": true,
        "npm-package-json-lint": npmPackageJsonLintConfig,
    },
};
```

Для включения правила нужно задать свойство `config.rules[ruleName]`; отдельные проверки могут потребовать дополнительной конфигурации (см. `npm-package-json-lint` в примере).

#### is-typescript

Проверяет, что в `devDependencies` пакета указан пакет `typescript`.

#### npm-package-json-lint

Проверяет, что `package.json` пакета соответствует указанным правилам. См. [npm-package-json-lint](https://npmpackagejsonlint.org).

#### npmrc-lint

Проверяет `.npmrc` в пакетах. Позволяет:
- Валидировать допустимые опции по белому списку (`allowedOptions`).
- Форсировать значения опций (`forcedOptions`). Поддерживаются только примитивные типы.

Пример конфигурации:

```javascript
module.exports = {
    rules: {
        "npmrc-lint": {
            allowedOptions: ["user-agent"],
            forcedOptions: {
                "package-json": false,
            },
        },
    },
};
```

Поддерживает опцию `--fix`.

#### common-dependencies

Проверяет, что версии зависимостей выровнены. Базовой версией всегда выбирается максимальная версия зависимости, найденная в монорепо. Дополнительно можно указать альтернативные допустимые версии зависимостей для групп пакетов.

Пример конфигурации:

```javascript
module.exports = {
    rules: {
        "common-dependencies": {
            groups: [{
                // Всем пакетам будет разрешено использование @yandex-int/tokenator@0.8.28
                packages: ["**"],
                alternativeVersions: {
                    "@yandex-int/tokenator": [
                        "0.8.28"
                    ],
                },
            }],
        },
    },
};
```

Поддерживает опцию `--fix`.

### Игноры

Игноры конфигурируются в `config.ignores`. Пример:

```javascript
const npmPackageJsonLintConfig = require('./npm-package-json-lint');

module.exports = {
    rules: {
        "is-typescript": true,
        "npm-package-json-lint": npmPackageJsonLintConfig,
    },

    ignores: [
        // Проверка "npm-package-json-lint" будет выключена для пакетов "@yandex-int/si.ci.*":
        { rules: ["npm-package-json-lint"], packages: ["@yandex-int/si.ci.*"] },

        // Помимо понятных игноров на основе имени пакета, `package-checker` умеет игнорировать правила
        // в зависимости от того, есть ли пакет в транке, или нет.
        //
        // Игнорируем обязательность typescript для пакетов, вкоммиченых в транк:
        { rules: ["is-typescript"], state: "present" },

        // А для "@yandex-int/si.ci.*" вдобавок отключаем проверку и для новых пакетов:
        { rules: ["is-typescript"], state: "new", packages: ["@yandex-int/si.ci.*"] },
    ],
};
```

Каждая маска в списке `config.ignores` строится следующим образом:

- `rules: Array<RuleName>` – список правил, которые нужно игнорировать.
- `packages?: Array<string>` – список глобов имён пакетов, которые нужно игнорировать.
- `state?: "new" | "present"` – требуемое состояние пакета:
  - `"new"` – правила не будут применяться для новых пакетов.
  - `"present"` – правила не будут применяться для уже существущийх пакетов.
  - по умолчанию – состояние пакета не учитывается.

`state` используется для возможности выключать некоторые правила в PR с новыми пакетами.

## Требования и ограничения

- `package-checker` использует [@yandex-int/package-selector](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/package-selector) для чтения графа пакетов.
- VCS, git или arc. Иначе игноры с `state: "new"` будут проигнорированы.
