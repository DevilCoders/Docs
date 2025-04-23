# @yandex-int/entrypoint-override

[eslint](https://eslint.org/)-правило для валидации конфигурации [экспериментальных адаптеров в web4](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/web4/docs/experiments/adapters.md). Напоминает установить параметр `__forceAssetPush` в `true`, когда это необходимо для предотвращения доставки лишнего кода на страницу.

Документацию по параметру `__forceAssetPush` можно найти [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/web4/docs/experiments/adapters.md?rev=r9033345#как-под-флагом-слать-только-экспериментальную-статику).

## Установка

1. Установить пакет

```sh
npm install --save-dev @yandex-int/entrypoint-override
```

2. Включить плагин и правило в конфигурации eslint

```json
{
  "plugins": [
    // ...
    "@yandex-int"
  ],
  "overrides": [
    // ...
    {
      // Включаем правило только для экспериментальных адаптеров
      "files": [
        "src/experiments/**/*.server.ts",
        "src/experiments/**/*.server.tsx"
      ],
      "rules": {
        "@yandex-int/entrypoint-override": "error"
      }
    }
  ]
}
```
