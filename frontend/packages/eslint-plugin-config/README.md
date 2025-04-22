# eslint-plugin-config

Стандартная конфигурация для ESLint из пакета @yandex-int/lint, оформленная по правилам плагинов ESLint
https://eslint.org/docs/latest/user-guide/configuring/configuration-files#using-a-configuration-from-a-plugin.

Это позволяет
- давать имена конфигурациям
- наследоваться от конфигурации, не указывая относительного пути с именем папки `./node_modules/`

## Установка

```bash
npm i -D @yandex-int/eslint-plugin-config --registry=https://npm.yandex-team.ru
```

## Использование

В файле `.eslintrc.js`:

``` json
{
    "extends": "plugin:@yandex-int/config/defaultConfig"
}
```

Обратите внимание, что префикс `eslint-plugin-` в название пакета ESLint подставляет автоматически.
