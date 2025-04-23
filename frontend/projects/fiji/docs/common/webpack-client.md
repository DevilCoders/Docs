# Клиентская сборка

Сборка клиентской статики происходит по платформам для указанных сервисов и использует [табурет](https://github.yandex-team.ru/serp/web4/blob/dev/src/lib/taburet/packages/react-ts-scripts/README.md).

## Получение текущих платформ

* В случае сборки через `npm run build...` платформа указывается как опция, а результат записывается в файл `.project`.
* В случае запуска сборки для котика - платформа считывается из файла `.project` в функции [getProjectTargets](https://a.yandex-team.ru/arc_vcs/frontend/projects/fiji/cli/helpers.js).

## Формирование опций для конфига webpack для текущей платформы
[К базовым настройкам добавляются](https://a.yandex-team.ru/arc_vcs/frontend/projects/fiji/sakhalin/src/vendors/taburet/build.js):
* текущий сервис
* текущая платформа
* entries для текущего сервиса и платформы с учетом экспериментальных уровней
* конфигурируется StaticCombineManifest для текущего сервиса и платформы

## Формирование платформенных конфигов webpack
Формирование конфигов зависит от типа сборки - [prod](https://a.yandex-team.ru/arc_vcs/frontend/projects/fiji/sakhalin/src/lib/taburet/packages/react-ts-scripts/config/webpack.config.prod.js) или [dev](https://a.yandex-team.ru/arc_vcs/frontend/projects/fiji/sakhalin/src/lib/taburet/packages/react-ts-scripts/config/webpack.config.dev.js).

## Процесс сборки статики
Процесс сборки зависит от окружения - [prod или dev](https://a.yandex-team.ru/arc_vcs/frontend/projects/fiji/sakhalin/src/lib/taburet/packages/react-ts-scripts/scripts/build.js)

## Кеширование результата обработки исходников
В процессе обработки каждого файла [формируется кеш](https://a.yandex-team.ru/arc_vcs/frontend/projects/fiji/sakhalin/src/lib/taburet/packages/react-ts-scripts/plugins/ci-cache-loader/index.js)

Кеш необходим для:
1. Переиспользования ранее собранных файлов (даже между несколькими запусками сборки);
2. Работы загрузчика [PlatformsRegistry](https://a.yandex-team.ru/arc_vcs/frontend/projects/fiji/sakhalin/src/lib/PlatformedRegistry/README.md), который вырезает из общеплатформенных файлов реализацию лишних платформ.

Результат кеширования сохраняется в папке `.build-cache/{platfrom}` и не зависит от сервиса

## Подготовка статики для загрузки на yastatic.net
Загрузка статики происходит в `sandbox-ci`, но для правильного процесса загрузки необходимо переложить собранные файлы в папку `freeze`.

Процесс перекладывая файлов происходит в [freezeAfterBuild](https://a.yandex-team.ru/arc_vcs/frontend/projects/fiji/sakhalin/src/lib/taburet/packages/react-ts-scripts/utils/freezeAfterBuild.js). Помимо базовых файлов тут происходит перекладывание манифеста для работы `Static Combine Server`.
