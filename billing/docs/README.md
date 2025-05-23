# Документация Биллинга
Данная документация описывает сервисы и процессы Биллинга.

## Расположение документации
[Testing](https://testing.docs.yandex-team.ru/billing/)

[Production](https://docs.yandex-team.ru/billing/)

## Разработка
Для начала необходимо ознакомиться с [документацией](https://docs.yandex-team.ru/docstools/) по YFM.

Для компиляции документации в .html файлы можно воспользоваться шорткатом `build-local`
```
➜ make build-local
...
Build time: 349.211ms
Ok
...
```

Тогда будет создана папка `/tmp/billing-docs` со скомпилированной документацей.
С помощью браузера нужно открыть файл index.html и посмотреть на результат компиляции.

При изменении документации достаточно заново запустить `build-local` и перезагрузить страницу в браузере.

Данную команду можно добавить в различные IDE, например в IDEA как конфигурацию и билдить документацию 1 шорткатом.
