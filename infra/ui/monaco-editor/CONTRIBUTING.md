## Установка

Выберите версию node и nvm
```shell
nvm use
```

Установите зависимости
```shell
npm i --force
```

`--force` нужен, чтобы проигнорировать конфликты peer версий пакетов.

## Разработка
В сторибуке
```shell
npm run storybook
```

## Сборка
```shell
npm run build
```

## Публикация
Используйте
```shell
npm run deploy
```
вместо стандартного `npm publish`, это необходимо, чтобы изменить package.json перед отправкой в npm
