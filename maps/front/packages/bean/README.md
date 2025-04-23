# @yandex-int/bean

Пакет для создания и работы реакций в виде бинарников в нирване.

## Quickstart

Для работы с пакетом понадобится установленный [ya tool](https://wiki.yandex-team.ru/yatool/distrib/) и [токен](https://oauth.yt.yandex.net/) для работы с YT.

```sh
npx @yandex-int/bean --registry="https://npm.yandex-team.ru" init <name>
```

Создает базовую структуру пакета, используя [шаблон](src/template). После создания можно сразу приступать к разработке. Не забудьте поменять `lama.yaml` конфиг в соответствии с вашими требованиями для запуска. [Подробнее про lama](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama#lama).

Добавьте необходимые переменные окружения в `jobVariables` в файле `lama.yaml` (см. [expressions](https://wiki.yandex-team.ru/nirvana/reactor/expression/)). **ВАЖНО**: в `expressions.globals` все списки и словари должны храниться однострочно (пока что, ждем фикса от команды реактора).

Пример:

```(yaml)
preset: projects/maps-front/binary-scheduler
preset_options:
  reaction_path: maps/front/maps/maps-devops-duty
  cron_expression: 0 0 * ? * *
  version: 1.1.0
  expressions:
    globals: global jobVariables = ["NO_DRY_RUN=1"].toStringList();
  globals:
    job-variables:
      type: VAR
      value: jobVariables
      value_type: PRIMITIVE_LIST_STRING
```

## У меня уже есть шедулер

[Документация по миграции](./docs/migration.md)

## Секреты

[Воркфлоу для запуска бинарника](https://nirvana.yandex-team.ru/flow/9e21896c-bb79-474f-938d-852d9e496876) уже содержит в себе [базовый набор секретов](https://yav.yandex-team.ru/secret/sec-01cjz1hw16ymy62e9f917k8gdk/explore/versions). Они лежат в соответствующих переменных окружения (общее соглашение: `{{SERVICE_NAME}}_OAUTH_TOKEN`)

```(js)
const startrekToken = process.env.STARTREK_OAUTH_TOKEN;
...
```

Если вам нужно использовать дополнительные секреты, создайте `.env` файл с вашими переменными окружения и [загрузите его as is в Нирвану](https://nirvana.yandex-team.ru/secrets) как `Private key`. Укажите название этого секрета в `environment-secrets` вместо строки `YOUR_NIRVANA_SECRET_ENV_FILE_HERE`.

Если вы хотите указать свой `workflow_id` — добавьте его в параметры пресета.

Пример:

```yaml
preset: projects/maps-front/binary-scheduler
preset_options:
  reaction_path: /maps/front/maps/your-scheduler-name
  nirvana_workflow_id: your-workflow-id
  globals:
    environment-secrets:
      type: CONST
      value: YOUR_NIRVANA_SECRET_ENV_FILE_HERE
  ...
```

## Публикация версий

Для публикации новой версии реакции-бинарника нужно обновить версию npm-пакета из командной строки: `npm version patch | minor | major`. В базовой структуре определены хуки, которые автоматически запустят `bean build -> bean tag -> bean upload`.

## Мотивация

Пакет был создан чтобы стабилизировать и значительно ускорить работу JS-шедулеров в Нирване.

Простейший npm-пакет, который запускается в Нирване требует установки зависимостей, которая [нередко падает](https://st.yandex-team.ru/GEOMONITORINGS/order:updated:false/filter?description=Reaction%20%2Fmaps%2Ffront), например, если моргнула сеть.

Также это небыстрый процесс. Для запуска npm-пакета нужен специальный слой с nodejs (еще и нужной версии nodejs и npm) и время на установку зависимостей в среднем занимает 3-4 минуты. Если требуется шедулер/реакция, которые должны обновлять информацию чаще — это реализовать невозможно базовыми методами.

Пакеты, собранные в бинарник и загруженные в нирвану через YT требуют < 30 секунд на холодный старт и в среднем около 15, если используется закешированный результат.
## How it works

`bean` основывается на пакете [pkg](https://www.npmjs.com/package/pkg). `pkg` позволяет собрать ваш npm-пакет в виде бинарника под выбранную платформу и версию nodejs. В общем случае все зависимости будут включены в него ([почти все](https://www.npmjs.com/package/pkg#config)).

`bean build [target] [output]` запаковывает собранный пакет (`package.json -> bin`), используя параметры `pkg`.

`bean tag` обновляет версию в `lama.yaml`, основываясь на `package.json` вашего пакета. Создает тег соответствующей версии.

`bean upload` загружает собранный бинарник в YT по пути https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/front/schedulers/binary/$REACTION_PATH/$PACKAGE_VERSION. Если загружено более 3 версий — самые старые удаляются автоматически (наличие 3 последних версий позволит быстро откатить шедулер в случае проблемного релиза, поменяв версию на предыдущую в `lama.yaml`).

Если ваш репозиторий находится в https://github.yandex-team.ru/maps, свежий `lama.yaml` опубликуется автоматически при влитии в основную ветку репозитория. Для проектов не в организации `maps` нужно добавить [вебхук в свой репозиторий](https://github.yandex-team.ru/maps/podrick-int/tree/master/server/projects/github#обновление-lamayaml-конфигов).

В реакторе по пути `${reaction_path}` создастся реакция, которая будет запускать [этот граф в Нирване](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama/presets/projects/maps-front/binary-scheduler.yaml#L10). При необходимости, можно склонировать граф и переопределить параметры `lama.yaml` обычным образом.
## Глобальные параметры

Для изменения пути до исходников в командах можно использовать переменную `path`. Путь должен указывать на корень пакета (где находится `package.json`).

```sh
npx @yandex-int/bean init --path ./your/custom/path
```

