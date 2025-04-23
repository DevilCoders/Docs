## Ответственные

  [@orange13](http://staff.yandex-team.ru/orange13)

## Структура проекта

    |-корень
      |-deps зависимости проекта
      |-source основная кодовая база (приложения django)
      |-build_and_push.sh скрипт заливки данных в registry

## Установка и запуск проекта

docker build .

## Запуск тестов

#### Заходим в папку с кодом
```cd source```
#### Запускаем тесты
```pytest```

## Пуш проекта в Qloud

#### Для пуша приложения в Qloud используем
```sh build_and_push.sh prod```
с ключем ```prod``` для **продакшен** Qloud