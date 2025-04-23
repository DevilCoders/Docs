# Структура проекта в idea

## Файлы и папки
В idea у проекта будет 2 папки.

* **generated** - папка со сгенерированными файлами (`BUILD_ROOT`). Здесь располагаются контроллеры, клиенты, код для работы с tvm и др. Код редактировать здесь нельзя (вы можете попробовать, но после регенерации все изменения исчезнут).

* **Папка с id сервиса** - это код вашего сервиса.

![](https://jing.yandex-team.ru/files/sid-hugo/image%20%2812%29.png)

### service.yaml
Главный конфигурационный файл фреймворка. Подробнее о нем и его формате можно почитать [здесь](configuration/service_yaml.md).

### ya.make.modules
Сюда фреймворк будет добавлять файлы с зависимостями для фич, которые были включены в `service.yaml`.

### generate_project.sh
Скрипт для запуска регенерации проекта. Аналог `ya ide idea`, только с запуском генерации с помощью MJ. Подробнее [здесь](about.md#Генератор-в-исходники-и-generate_project.sh).

### api.yaml
OpenApi спецификацию своего сервиса можно положить в `src/main/resources/openapi/api/api.yaml`. Если расположение этого файла отличается, то необходимо указать это в [service.yaml](configuration/service_yaml.md#serveropenapispecpath)

## Run configurations
Так же в проекте будут доступны две `run configurations`:
- **Run Service (generated)** - конфигурация для запуска сервиса
- **Regenerate project (generated)** - для перегенерации проекта
![](https://jing.yandex-team.ru/files/sid-hugo/image%20%2813%29.png)

