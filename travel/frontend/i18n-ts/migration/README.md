# Migration

Здесь представлен пример миграции с помощью [jscodeshift](https://github.com/facebook/jscodeshift)
cо старого пакета `ymaps-tanker` (deprecated, потерян где-то в недрах заблокированного github) работы с ключами на новый подход c TS модулями.

## Disclaimer

Миграция сильно зависит от вашего проекта,
эта миграция с ymaps-tanker представлена здесь для примера.
Файл `migration/ymaps-tanker.js` содержит код миграции.
Файлы `migration/__testfixtures__/*.input.ts(x)` содержат примеры исходных файлов.
Файлы `migration/__testfixtures__/*.output.ts(x)` содержат примеры файлов после миграции.

## Getting started

Установить jscodeshift глобально:

```
npm install -g jscodeshift
```

Вызвать миграцию (указать папку для миграции и скрипт миграции)

```
jscodeshift src/ -t migration/ymaps-tanker/ymaps-tanker.js --extensions=tsx,ts,js,jsx
```
