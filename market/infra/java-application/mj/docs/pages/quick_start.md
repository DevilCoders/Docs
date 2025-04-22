# Как начать пользоваться

{% note warning %}

Мы не поддерживаем 8-ю версию Java. Поэтому, если вы создаете у себя сервис на MJ, то папка, в которой вы это делаете, не должна быть подключена к сборке на JDK 8

{% endnote %}

## Как опробовать фреймворк
Чтобы быстро создать папку с сервисом на MJ, достаточно воспользоваться командой [ya project create MJ](ya_project.md#ya-project-create-mj).

## Создание нового сервиса 
Для создания сервиса с фреймворком, достаточно выбрать соответствующий шаблон в СПОКе
![](https://jing.yandex-team.ru/files/sid-hugo/image%20%283%29.png)

После того, как в аркадии создастся проект, его можно будет открыть в IntelliJ IDEA. Для этого нужно:
1) Подтянуть изменения с транка
```
arc pull trunk
```
2) У себя на компьютере в смонтированной аркадии перейти в папку с этим проектом
```
cd <путь до аркадии>/<путь до только что созданного проекта>
```
3) Запустить `generate_project.sh`:
```
./generate_project.sh <здесь можно указать папку, в которой создать проект для idea>
```
4) Открыть с помощью Intellij Idea папку с проектом (если на предыдущем шаге путь до папки не указывали, то проект будет лежать в папке `~/idea_projects`)
5) Готово

## Перевоз существующего сервиса 
Чтобы перевезти существующий сервис, необходимо проделать несколько шагов (а если что-то не получается или непонятно, то можно приходить к [нам в чат](https://t.me/joinchat/RImGNXqbohFkOTg6 ))

### С помощью скрипта 
1. **Запустить [скрипт](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/mj/v1/generate-project-tool/transfer_templates.sh?rev=trunk)** (запуск скрипта можно осуществить из любой директории):
```
./transfer_templates.sh -a /path/to/arcadia -p /path/to/service -r root.package.of.project -t TRACE_MODULE
```

Флаги запуска:
   - **-a** _(необязательный)_ — путь до аркадийной дириктории (по умолчанию `/Users/user/arcadia`)
   - **-p** _(обязательный)_ — путь до директории проекта, который перевозите
   - **-r** _(обязательный)_ — root package вашего проекта (Например, `ru.yandex.market.my.frameworktest`)
   - **-t**  _(обязательный)_ — Название  trace module сервиса (уже существующий, который находится в [Module.java](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/request/request-utils/src/main/java/ru/yandex/market/request/trace/Module.java) или новый, который будет туда помещен (Назавние пишется через `Caps Lock`, для разделения слов используйте `_`. )
   
В результате будут добавлены следующие файлы в корень проекта (на уровне с основным ya.make):
![](https://jing.yandex-team.ru/files/sid-hugo/image%20%284%29.png)

И директория openapi.api (по пути `src/main/resources`), в которую необходимо будет поместить `api.yaml`.

![](https://jing.yandex-team.ru/files/sid-hugo/image%20%285%29.png)
   
   Также в `ya.make` будут добавлены несколько строчек:
```
SET(MJ_VERSION v1)
INCLUDE(${ARCADIA_ROOT}/market/contrib.ya.make)
INCLUDE(${ARCADIA_ROOT}/market/infra/java-application/mj/${MJ_VERSION}/mj.ya.make)
```

2. **Описать ваш api в файле [api.yaml](how_it_works/configuration/api_yaml.md)**
   
Упростить этот процесс может библиотека springfox. Достаточно добавить себе [такие временные строчки кода](https://gist.githubusercontent.com/musibs/8bdefd8e97c529c576e7796768e8f213/raw/7f49fedb2ee377b9391012f7ab6e4bc8bda45115/SwaggerConfiguration.java) (не забудьте указать там ваш `basePackage`). 
После этого можно запустить сервис и вытащить openapi спеку по вашим ручкам по пути `/v2/api-docs`. Подробнее можно почитать [тут](https://medium.com/swlh/how-to-create-a-node-rest-stub-with-swagger-codegen-b419080559cf).

3. **Запустить generate_project.sh**
```
./generate_project.sh <здесь можно указать папку, в которой создать проект для idea>
```
4. Открыть с помощью Intellij Idea папку с проектом (если на предыдущем шаге путь до папки не указывали, то проект будет лежать в папке `~/idea_projects`)

### Перевоз руками 
Все те же шаги, что делает [скрипт](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/mj/v1/generate-project-tool/transfer_templates.sh?rev=trunk) можно проделать самому
1. Добавить файл [service.yaml](how_it_works/configuration/service_yaml.md) в корень кода сервиса. (Если у сервиса нет trace модуля, нужно добавить его в файл [Module.java](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/request/request-utils/src/main/java/ru/yandex/market/request/trace/Module.java))
2. Добавить [package.json](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/templates/mj-template/package.json)
3. Добавить туда же этот файл [generate_project.sh](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/java-application/templates/mj-template/generate_project.sh)
4. Добавить в `ya.make`:
```   
SET(MJ_VERSION v1)
INCLUDE(${ARCADIA_ROOT}/market/contrib.ya.make)
INCLUDE(${ARCADIA_ROOT}/market/infra/java-application/mj/${MJ_VERSION}/mj.ya.make)
```
5. Вернуться ко второму пункту [первого способа](#с-помощью-скрипта)

## Kotlin
Если ваш сервис написан на Kotlin, не забудьте добавить в `service.yaml` поле [java_service.lang](how_it_works/configuration/service_yaml.md#lang) со значением `kotlin`:
```yaml
java_service:
  lang: kotlin
```
