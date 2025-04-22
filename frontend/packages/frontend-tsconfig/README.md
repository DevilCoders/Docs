#frontend-tsconfig

Общие конфигурации typescript для проектов монорепозитория поисковых интерфейсов

## Использование

```json
{
  "extends": "@yandex-int/frontend-tsconfig",
  "compilerOptions": {
    "outDir": "./build/",
    "rootDir": "./src/",
    "typeRoots": [
      "./node_modules/@types/",
      "./src/typings/"
    ]
  },
  "include": [
    "./src/**/*"
  ],
  "exclude": [
    "./src/**/*.test.ts"
  ]
}
```
