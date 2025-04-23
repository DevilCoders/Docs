# arc-filepath-linters

Универсальный линтер имён файлов для репозиториев синхронизируемых arc.

## Установка

```console
npm i [-g] @yandex-int/arc-filepath-linters --registry=https://npm.yandex-team.ru
```

## Использование в качестве cli-утилиты

Проверить свой git-репозиторий на наличие проблемных файлов для arc VCS можно с помощью cli-утилиты (после установки пакета глобально: `npm i -g`):

```console
arc-lint </path/to/repo>
```

## Использование в качестве линтера в lint-staged проверках

Линтер построен на системе плагинов.
Пример кода использования:

```javascript
import chalk from "chalk";

import lint from "@yandex-int/arc-filepath-linters";


async function main() {
    // пути файлов должны быть указаны относительно корня репозитория,
    // а не относительно cwd
    const items = [
        "frontend/services/weather/package.json",
        "frontend/services/ydo/index.js",
    ];
    try {
        await lint(items, [
            // список используемых плагинов для линтера
            { id: "trailing-spaces" },
            { id: "no-same-names" },
            { id: "no-vcs-meta" },
            { id: "unsafe-symbols" },
            { id: "windows-safe" },
            { id: "no-symlink" }
        ]);
    } catch (error) {
        console.error(chalk.red(error));
        process.exit(1);
    }
}

main();
```

## Список поддерживаемых плагинов

* `unsafe-symbols`: Плагин на запрещённые символы в именах файлов
* `trailing-spaces`: Плагин пробельные на символы в начале и конце названия файлов/директорий. [ARCADIA-23]
* `no-vcs-meta`: Плагин на проверку не совпадения имен с VCS meta файлами (`.git`, `.arc`, …). [DEVTOOLS-2278]
* `windows-safe`: Плагин на зарезервированные Windows ОС имена файлов. [DEVTOOLS-2073]
* `no-same-names`: Плагин на проверку регистронезависимой уникальности имён файлов и директории. [DEVTOOLS-2397]
* `no-symlink`: Плагин на проверку наличия симлинков. Симлинки в аркадии запрещены.

[ARCADIA-23]: https://st.yandex-team.ru/ARCADIA-23
[DEVTOOLS-2278]: https://st.yandex-team.ru/DEVTOOLS-2278
[DEVTOOLS-2073]: https://st.yandex-team.ru/DEVTOOLS-2073
[DEVTOOLS-2397]: https://st.yandex-team.ru/DEVTOOLS-2397
