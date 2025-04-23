# tide-experimenter

Плагин к tide для автоматизации работы с экспериментами.

## Использование
### Генерация тестов экспериментов
Команда `exp` (алиас `exp:create`), позволяет создать эксперимент с нуля либо с использованием существующего кода.
```
tide exp [source-path] --exp-name <string> [...options]
```

`source-path` — путь, откуда будут копироваться файлы.
В случае отсутствия будут сгенерированы файлы с базовой структурой тестов.

`--exp-name <string>` — имя эксперимента. Обязательный параметр.
Используется при построении пути к эксперименту, а также для заполнения полей `experiment` в hermione и testpalm файлах.

`--exp-flags <query-string>` — флаги эксперимента в формате query string.
Флаги будут проставлены в вызовы указанных в конфиге `commandNames`, а также в `params` в testpalm.

`--exp-flags-json <json>` — флаги эксперимента в формате json.
Если заданы оба параметра, флаги в формате json перезаписывают значение предыдущей опции.

`--copy-testdata` — определяет, нужно ли переносить данные тестов из `source`.

`--copy-screens` — определяет, нужно ли переносить скриншоты из `source`.

`--copy-assets` — выставляет `--copy-testdata` и `--copy-screens` в `true`.

Директория назначения генерируется автоматически. Для старого стека структура имеет вид `experiments/<exp-name>/FeatureName/FeatureName.test/`. Для нового - `src/experiments/<exp-name>/FeatureName/FeatureName.test/`.

#### Примеры использования
```
tide
    -c tide.config.js
    exp
    src/features/FeatureName/FeatureName.test
    --exp-name "Experiment-1"
    --exp-flags "new_flag=22"
```
В этом случае будет создан эксперимент в директории `src/experiments/Experiment-1/features/FeatureName/FeatureName.test/` основе тестов в директории `src/features/FeatureName/FeatureName.test`.

### Раскатка экспериментов
Команда `exp:merge` позволяет выполнить раскатку эксперимента — перенести тесты с experiment уровня на production, удалить флаги из запросов и дампов, перенести скриншоты, дампы и файлы метрик.
```
tide exp:merge <source-path> [...options]
```
`source-path` — путь к файлам эксперимента, откуда будут копироваться тесты и данные.

`--target-dir` — путь к директории с файлами на production уровне.
По умолчанию: интерактивный запрос соответствующего файла в production для каждого файла на экспериментальном уровне.

`--remove-flags` — список флагов через запятую, которые нужно удалить из запросов и дампов.

#### Примеры использования
```
tide
    -c tide.config.js
    --conflict-mode new
    exp:merge
    src/experiments/FeatureName/FeatureName.test
    --target-dir src/features/FeatureName/FeatureName.test
    --remove-flags direct_label,hideads
```
В этом случае тесты, скриншоты и дампы будут скопированы из директории `src/experiments/FeatureName/FeatureName.test` в `src/features/FeatureName/FeatureName.test`.
При возникновении конфликтов старые элементы будут заменены на новые — с экспериментального уровня (`--conflict-mode new`).
Из дампов и запросов будут удалены флаги (`--remove-flags direct_label,hideads`).

## Конфигурация
Пример `tide.config.js`:
```js
module.exports = {
    plugins: {
        'tide-experimenter': {
            enabled: true,
            commandNames: ['yaOpenSerp'],
        },
        // ...
    },
};
```
### `(optional) commandNames: string[]`
Массив hermione команд, в аргументы которых будут проставлены флаги эксперимента.

По умолчанию: `['yaOpenSerp]`. 
