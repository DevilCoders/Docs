# Настройки генерации

## Пользовательская настройка флагов для ya ide idea
При необходимости добавить флаги к обычному запуску `ya ide idea`, можно воспользоваться Script options в `Run/Debug Configurations` (Edit Configurations → Script options). Все дополнительные флаги прячутся за флагом `-ideflags` и далее пишутся в кавычках. 
Пример: `-ideflags “-DHAVE_CUDA=no”`

Внутренние кавычки экранируются слешем `\”`
![](https://jing.yandex-team.ru/files/sid-hugo/image%20%289%29.png)

![](https://jing.yandex-team.ru/files/sid-hugo/image%20%2810%29.png)

При необходимости использования собственной команды запуска, ее можно прописать в `service.yaml`.
```yaml
java_service:
  ya_ide: ya ide idea --iml-in-project-root --local --directory-based --with-content-root-modules --yt-store --group-modules=tree -DJDK_VERSION=11 --project-root /Users/katejud/idea_projects/my-framework-test-service2
```

Для генерации проекта в папку, указанную в ключе -i generate_project.sh, можно воспользоваться переменной конструкцией `--project-root {IDEA_PROJECT_DIR}`. `{IDEA_PROJECT_DIR}` автоматически заменится на директорию указанную при генерации проекта (или на дефолтную директорию idea_projects).

Также через поле `ya_ide` можно прописать только дополнительные флаги:
```yaml
java_service:
  ya_ide: -DCUDA_HOST_COMPILER=/usr/bin/gcc-6.1 -DCUDA_NVCC_FLAGS=--use_fast_math
```

Будет полезно упомянуть, что для того, чтобы дополнительно в проект добавлялись исходники из других директорий аркадии, можно воспользоваться флагом -С (стандартным флагом для ya ide idea):
```yaml
java_service:
  ya_ide: -C . ../mbi-dwh-common ../mbi-dwh-migrations ../mbi-dwh-proto ../../../jlibrary/yt-dyn-tables-utils
```
Пути указываются относительно корневого проекта (в данном случае `market/mbi/mbi-dwh/data-aggregator`).

## Настройка генерации исходников
Во время генерации проекта, на основе `service.yaml` в код сервиса может добавлятся различный функционал.
Это могут быть:
* заглушки для реализации ручек, сгенерированных на основе `api.yaml`.
* зависимости для подключаемых модулей
* шаблонные тесты модулей и примеры кода

Эту дополнительную генерацию можно отключить или генерировать эти файлы не сразу в папке аркадии, а во внешней папке (и потом самостоятельно выборочно добавить в код сервиса то, что считается нужным).

Сконфигурировать в `service.yaml` можно так:
```yaml
#arcadia/folder/disable
generation_settings:
  ya_make_dependencies: arcadia
  modules_templates: folder
  api_service_classes: disable
```

* ya_make_dependencies - отвечает за генерацию зависимостей для модулей
* modules_templates - отвечает за генерацию шаблонного кода/тестов модулей
* api_service_classes - отвечает за генерацию заглушек реализации ручек

Доступны 3 значения у этих параметров:
* `arcadia` - генерация непосредственно в папу аркадии
* `folder` - генерация во внешнюю папку
* `disable` - отключает генерацию выбранной категории

Внешняя папка по умолчанию `<папка_с_проектом_идеи_(default:idea_projects)>/mj-generated/<имя_сервиса>`.
Ее можно изменить, если в скрипт генерации передать параметр `-g <моя/кастомная/папка>`

## Добавление новых файлов в arc

По умолчанию, генерируемые файлы добавляются в vcs командой ``arc add``.
Для отключения этой фичи, в скрипт перегенерации проекта (Regenerate project) необходимо добавить флаг ``-novcs``.
