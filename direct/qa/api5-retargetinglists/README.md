# Тесты на api5
https://tech.yandex.ru/direct/doc/ref-v5/concepts/about-docpage/

## Запуск тестов
Чтобы запустить, нацелившись на бету, нужно написать в `direct.test.run.properties`:

```ini
stage.type: BETA6
direct.stage=13885
```

## Инструменты

### Рекомендатор
Для работы с тестовыми данными есть сервис _Рукояточник_: https://direct-handles.qart.yandex-team.ru/index.html
В нем можно поискать/поредактировать все тестовые данные.

### Robomongo
Для просмотра данных в монге можно поставить себе robomongo https://yadi.sk/d/Hj-dmf4v3NTkrW и через него смотреть записи по базе
Настройки можно поставить такие
https://jing.yandex-team.ru/files/silver/2017-10-03_16-19-02.png
