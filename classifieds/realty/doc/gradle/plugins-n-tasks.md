# Полезные плагины и таски gradle

### DockerPreparePlugin

Плагин, который генерирует все необходимые файлы для дальнейшей упаковки сервиса в докер.

Для его подключения необходимо:

1. Добавить в манифест деплоя параметр переменные `XMX`, `GC_OPTIONS`, `JVM_OPTIONS`. Например:
   ```
   XMX: 3G
   GC_OPTIONS: -XX:+UseG1GC -XX:+AlwaysPreTouch
   JVM_OPTIONS: -XX:ActiveProcessorCount=8
   ```
2. Добавить в `build.gradle` сам плагин и его настройку
   ```groovy
   import ru.yandex.realty.gradle.DockerPreparePlugin
   apply plugin: DockerPreparePlugin
    
   // other settings

   // serviceName:
   //   Влияет на:
   //     - путь, куда будут собраны все jar зависимости
   //     - имя стартового скрипта 
   //     - имя процесса сервиса
   // appMainClass:
   //    Используется для запуска сервиса:
   //      java [PARAMS] $appMainClass
   // resources:
   //    Map - опицональный параметр, в котором ключ является путем откуда скопировать ресурсы, а
   //    значением - путь куда положить относительно корня докер приложения. Например, если указать 
   //
   //    resources = ['folder1': 'usr/folder1', 'folder2': '/usr/folder2']
   //
   //    То в результате структура в докере будет: 
   //
   //    /
   //    ├── usr
   //    |   ├── folder1
   //    │   ├── folder2
   //    
   // startupScriptPath:
   //    Путь до sh-ка от корня модуля. Служит для плавного перехода на сгенеренные скрипты.
   //    При его использовании не будет генерироваться Dockerfile. Опцию appMainClass можно не указывать.
   //
   dockerApp {
    serviceName = "service-name"
    resources = ['../yandex-realty2-resources/resources': '/var/lib/yandex/realty2/resources']
    // startupScriptPath = 'assembly/serrvice-name.sh'
   }
   ```

В результате сервису добавятся таски:

1. `collectJars` - собрать все зависимости
2. `generateDockerScripts` - сгенерировать Dockerfile и стартовый bash скрипт
3. `prepareDocker` - выполнить 1 и 2 таски

### MakeLocalConfigPlugin

Для его подключения необходимо:

1. Установить [shiva-conf](https://github.com/YandexClassifieds/shiva-conf)
2. Задать токен
   для [секретницы](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982)
   в переменную окружения `VAULT_API_TOKEN`
   ```bash
   # как вариант можно задать переменную временно так
   export VAULT_API_TOKEN=тут_буковки_токена
   ```
3. Прописать в ```build.gradle``` следующее, с указанием нужных значений в параметры
   ```groovy
   import ru.yandex.realty.gradle.config.MakeLocalConfigPlugin
   
   apply plugin: MakeLocalConfigPlugin
   
   localConfig {
    shivaServiceName = "my-service"                     // f.e. realty-feeds
    configFileName = "conf_name_without_extension"      // feeds for "feeds.conf"
   }

   ```
4. Вызвать
   ```bash 
   ./gradlew :my-service:makeLocalConfig
    ```

В результате локальный конфиг будет по пути ```service-dir/src/main/reasources/{service-name}.local.conf```. Если
локальный конфиг уже был, то все изменения в нем удалятся

Если плагин не видит shiva-conf проще всего сделать на него симлинк

   ```bash
   # сначала положил shiva-conf в каталог bin текущего пользователя 
   ln -s ~/bin/shiva-conf /usr/local/bin/
   ```

Почти наверняка у локального конфига будет какой-то инклуд общего конфига, тогда нужно будет этот общий конфиг также сгенерить и заменить его имя в инклуде на локально сгенеренный.
Также, почти наверняка, рядом будет лежать development.config с настройками для тестинга, который нужно заинклудить в конце свежесгенерированного конфига.