## @yandex-int/eslint-plugin

Пакет с кастомными плагинами для eslint.

### Установка

`npm i -S @yandex-int/eslint-plugin --save-dev`

### Использование

Хотим заиспользовать `NAMEPLUGIN` из пакета.
В проектном `.eslintrc.json` добавляем:

```json
{
    "plugins": [
        "@yandex-int"
    ],
    "rules": {
        "@yandex-int/NAMEPLUGIN": ["error", options]
    }
}
```

### Разработка

Устанавливаем зависимости: `npm i`
Запускаем тесты: `npm test`

Хотим сделать новый `NAMEPLUGIN`:
- создаём папки `(lib|docs|tests)/rules/NAMEPLUGIN`
- создаем файлы `NAMEPLUGIN.(js|md|js)`, в каждую папку из предыдущего шага
- в корневом `index.js` экспортируем `NAMEPLUGIN: require('./lib/rules/NAMEPLUGIN'),`
