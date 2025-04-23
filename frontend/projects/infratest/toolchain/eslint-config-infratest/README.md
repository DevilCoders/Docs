# Конфиг eslint для typescript

**Этот конфиг подходит только для typescript**

## Package.json

```json
{
    "scripts": {
        "lint": "npm run eslint",
        "eslint": "eslint src --ext .ts",
        "reformat": "eslint src --ext .ts --fix"
    },
    "devDependencies": {
        "@typescript-eslint/parser": "x",
        "@yandex-int/eslint-config-infratest": "x",
        "eslint": "x"
    },
    "eslintConfig": {
        "extends": [
            "./node_modules/@yandex-int/eslint-config-infratest/index.js"
        ]
    }
}
```

Здесь `x` означает те версии, которые приняты в монорепо. Это могут быть разные версии для разных пакетов.

Полный путь в конфиге нужен из-за hoisting. Сейчас плагины в eslint загружаются при помощи `require`:
```
root
    node_modules
        eslint
            require("@yandex-int/eslint-config-infratest")
    packages
        package
            node_modules
                @yandex-int
                    eslint-config-infratest <- не может быть достигнут из eslint
```
