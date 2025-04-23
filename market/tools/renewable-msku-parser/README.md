## Парсер для частотных товаров

Утилита преобразует входной файл в формате .xls/.xlsx в protobuf-бинарник, попутно обогощая информацией о категории и модели из ЫТя.
В excel-файле обязательно должны присутствовать следующие поля: `msku` и `repurchasePeriod`, названия которых дожны быть указаны в заголовке (первой строке) файла.


### Сборка и запуск
Для программы тербуется доступ в YQL (обогащение данных из YT) и Sandbox (загрузка ресурсов в облако).
Доступ осуществляется при помощи OAuth-токенов авторизации.

Токен для YQL можно здесь: https://yql.yandex-team.ru/?settings_mode=token
и сохранить в файл `~/.yql/token`.
```bash
$ mkdir -p ~/.yql ; chmod 700 ~/.yql ; echo 'вставте_сюда_свой_токен' > ~/.yql/token ; chmod 400 ~/.yql/token
```
Также токен можно передать через параметр `-Dapp.yql_token=вставте_сюда_свой_токен` 

Аналогично для Sandbox. Нужно получить токен: https://sandbox.yandex-team.ru/oauth/ 
и сохранить в в файл `~/.sandbox/token`.
```bash
$ mkdir -p ~/.sandbox ; chmod 700 ~/.sandbox ; echo 'вставте_сюда_свой_токен' > ~/.sandbox/token ; chmod 400 ~/.sandbox/token
```
Также токен можно передать через параметр `-Dapp.sandbox_token=вставте_сюда_свой_токен`
___
Для сборки следуют счекаутить проект к себе на машину, установить maven и запустить команду 
```bash
$ ya make -r
```
___
После этого в текущей директории появится файл `tools-renewable-msku-parser.jar`. Запускаем приложение следующей командой:
```bash
$ java -cp %filename.jar% -Dapp.input=%path/to/directory/with/files% [-Dapp.output=%path/to/output/dir%] [-Dapp.user=%username%] [-Dapp.yql_token=%YQL-token%] [-Dapp.sandbox_token=%sandbox-token%] [-Dapp.upload=true] ru.yandex.market.freqparser.App 
```
#### Пример
```bash
$ java -cp tools-renewable-msku-parser.jar -Dapp.input=/Users/name/data -Dapp.env=prod -Dapp.upload=true ru.yandex.market.freqparser.App
```

#### Обязательные параметры
`-Dapp.input` - путь к папке которая содержит файлы .XLSX" или *.XLS с перчнем частотных товаров.
#### Не обязательные параметры
Если не указывать директорию для выходного файла (`-Dapp.output`), утилита создаст его в директории с входящими файлами.  
Если не передать флаг `-Dapp.upload`, бинарник не будет загружен в Sandbox.  
Необходимо передать флаг `-Dapp.env=prod`, если необходимо получить данные для продуктовых данных.
Иначе загрузятся данные из тестовых таблиц.  
Если передать флаг `-Dapp.user` то имя пользователя будет взято из параметра. Иначе из ОС.  
Если передать флаг `-Dapp.yql_token` то токен будет взят из параметра. Иначе из файла `~/.yql/token`.   
Если передать флаг `-Dapp.sandbox_token` то токен будет взят из параметра. Иначе из файла `~/.sandbox/token`.   

Выходной файл будет формата `renewable_mskus_yyyyMMdd-HHmmss.pb.bin`, содержащий внутри бинарного вида данные после сериализации в формат protobuf.
