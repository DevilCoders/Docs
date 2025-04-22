# palmsync-expflags-validator

> Плагин для [`palmsync`](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/palmsync), проверяющий использование экспериментальных флагов в тест-кейсах.

## Зависимости

* Node.js 8.6+
* npm

## Использование

Установите плагин в вашем сервисе.

```bash
npm install -D @yandex-int/palmsync-expflags-validator --registry=https://npm.yandex-team.ru
```

Добавьте плагин в конфигурационный файл `.palmsync.conf.js`.

```js
{
  // …
  plugins: {
    validate: {
      '@yandex-int/palmsync-expflags-validator': {
        patterns: ['./expflags/*.json']
      },
      // …
    },
  //…
  }
}
```

Настройка завершена. Теперь можно выполнить команду `palmsync validate`, чтобы запустить валидацию тест-кейсов.

## Опции

### `enabled`

* Type: `boolean`
* Default: `true`

Позволяет включить или выключить плагин без его удаления из конфига.

### `patterns`

* Type: `string[]`
* Default: `['./expflags/.json']`

Паттерны, по которым будут получены декларации флагов из сервиса.

Подробнее про хранение флагов в коде сервиса можно почитать в [документации к expflags-cli](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/expflags-cli#%D1%85%D1%80%D0%B0%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B4%D0%B5%D0%BA%D0%BB%D0%B0%D1%80%D0%B0%D1%86%D0%B8%D0%B9-%D1%84%D0%BB%D0%B0%D0%B3%D0%BE%D0%B2).

### `flagsPropertyName`

* Type: `string`
* Default: `exp_flags`

Имя параметра, в котором указаны используемые в тест-кейсе флаги.

### `rules`

* Type: `object`
* Default: `{}`

Управление правилами валидации. Позволяет включать и отключать правила, используя их имена, а также передавать в них опции, если правило их поддерживает.

Пример отключения одного из правил:

```js
{
  // Отключает правило.
  "NoUndeclaredFlagRule": false
}
```

Пример передачи опций в правило:

```js
{
  // Включает правило и передаёт в него опции.
  "NoUndeclaredFlagRule": [true, { ignore: ["rear"] }]
}
```

Если опция не указана, либо её значение равно `{}`, то все опции будут включены по умолчанию.

## Правила валидации

### `NoUndeclaredFlagRule`

Правило проверяет, что используемый флаг в тест-кейсе имеет декларацию в сервисе. Декларации флагов извлекаются из JSON-файлов на основе паттернов, указанных в опции [`patterns`](#patterns).

Правило поддерживает следующие опции:

* `ignore` — Имена флагов, для которых наличие деклараций в сервисе не будет проверяться.

Пример настроек:

```js
{
  // Игнорирует отсутствие декларации для флага `flag_name` в сервисе.
  "NoUndeclaredFlagRule": [true, { ignore: ["flag_name"] }]
}
```

Пример ошибки:

```
The 'button_color' flag not found in flag declarations. Please add a flag declaration to the service.
```

### `NoUndeclaredFlagValueRule`

Правило проверяет, что используемое значение флага в тест-кейсе имеет декларацию в сервисе. Декларации флагов извлекаются из JSON-файлов на основе паттернов, указанных в опции [`patterns`](#patterns).

Пример ошибки:

```
The 'button_color' flag declaration has no value '#fff' in the 'values' field. Please specify a value in the flag declaration (file: ./expflags/button_color.json).
```

### `NoUndefFlagValueRule`

Правило проверяет, что используемый флаг в тест-кейсе имеет значение.

Пример корректного тест-кейса:

```yaml
specs:
  Корректный тест-кейс:
    params:
      exp_flags:
        - button_color=#fff
```

Пример некорректного тест-кейса:

```yaml
specs:
  Некорректный тест-кейс:
    params:
      exp_flags:
        - button_color
```

Возникающая ошибка валидации:

```
Incorrect use of the 'button_color' flag. The flag value is required. Please specify a value (button_color=<value>).
```

### `NoCombinedFlagsRule`

Правило проверяет, что используемый флаг не является комбинированным. Комбинированным флагом считается строка, содержащая два и более флагов, разделённый через `;`.

Пример корректного тест-кейса:

```yaml
specs:
  Корректный тест-кейс:
    params:
      exp_flags:
        - button_color=#fff
        - header_background=#000
```

Пример некорректного тест-кейса:

```yaml
specs:
  Корректный тест-кейс:
    params:
      exp_flags:
        - 'button_color=#fff;header_background=#000'
```

Возникающая ошибка валидации:

```
The use of the combined flag was found. Please specify flags (button_color, header_background) separately.
```

### `FlagValueTypeCorrectnessRule`

Правило проверяет, что значение, указанное у флага в YAML-файле имеет корректный тип. Проверка типа осуществляется на основе типа, указанного в поле `validation_type` в декларации флага.

Пример корректного тест-кейса:

```yaml
# Флаг `button_color` имеет тип `str`
specs:
  Корректный тест-кейс:
    params:
      exp_flags:
        - button_color=#fff
```

Пример некорректного тест-кейса:

```yaml
# Флаг `button_color` имеет тип `bool`
specs:
  Корректный тест-кейс:
    params:
      exp_flags:
        - button_color=1  # Должно быть `button_color=true
```

Возникающая ошибка валидации:

```
The 'button_color' flag has the 'bool' type, but the specified value (1) does not match this type. Examples of valid values: true, false
```
