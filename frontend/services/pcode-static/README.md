# Статические файлы Показывающего кода
Репозиторий содержит ресурсы необходимые для деплоя статический файлов в S3. Файлы кешируются на 30 лет. Снаружи доступны по адресу https://yastatic.net/pcode-static/*

### Как задеплоить
В любом из шаблонов нужно нажать кнопку "Launch new task"
Перед деплоем не забыть влить свой код в trunk
Узнать последнюю выгруженную версию можно так https://s3.mds.yandex.net/pcode/static/versions.json

## Измерители
Внешние измерители видимости.

### Сборка
```bash
npm run build:measurers
```
### Деплой
[Шаблон таски в Sandbox](https://sandbox.yandex-team.ru/template/PCODE_STATIC_DEPLOY_MEASURERS/)
### Пример файла
[S3](http://s3.mds.yandex.net/pcode/static/measurers/1/main.js)

## Ресурсы
Статические файлы
### Сборка
Не требуется
### Деплой
[Шаблон таски в Sandbox](https://sandbox.yandex-team.ru/template/PCODE_STATIC_DEPLOY_RESOURCES/)
### Пример файла
[S3](http://s3.mds.yandex.net/pcode/static/resources/11/dummy.png)
