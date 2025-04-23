Сборка: `../gradlew build` 
Проект зависит от внутренних библиотек Яндекса (ссылается на artifactory.yandex.net), поэтому можно исключить из сборки опцией -PdisableYandexModules=true

Для идеи установить плагин Lombok и настроить tvm

Запуск локально из папки `/servicebus`:  
- из идеи:
  Run на классе ServicebusApp, VM Options: ```-Djava.library.path=~/arc/arcadia/bin -Denv.config=../properties/local/local.properties```
- в терминале:
  - `../gradlew bootRun `

Доступно здесь: `http://localhost:8382//servicebus` 
