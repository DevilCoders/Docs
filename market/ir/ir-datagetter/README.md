# ir-datagetter

Выгружает данные по моделям из YT

## Разработка

### Начало работы

Для начала работы сгенерируйте проект с помощью скрипта:

```sh
./scripts/create-project.sh
```

Если вы используете структуру папок из [этой инструкции](https://wiki.yandex-team.ru/users/sulim/howto/arc-directory-structure/),
то генерация проекта будет выглядеть так:

```shell script
ya ide idea --iml-in-project-root --project-root ~/arc/idea-projects/market/ir/ir-datagetter
```

Затем откройте сгенерированный проект в  idea.

### Локальная сборка и тесты из консоли

Для сборки и запуска тестов из консоли наберите:

```sh
ya make -ttt .
```

## Локальный запуск

Для локального запуска наберите в консоли

```sh
./run.sh ru.yandex.market.ir.datagetter.AppCli --yt-cluster hahn --ir-service matcher --mbo-export-path //home/market/production/mbo/export/recent --cats 90404
```

## Сборка и деплой в ЦУМ

Добавлен пайплайн [IR-Datagetter](https://tsum.yandex-team.ru/pipe/projects/ir/delivery-dashboard/ir-datagetter) для
сборки и выкладки market-ir-datagtter.jar в виде ресурсов sandbox.

Для тестинга ресурс _MARKET_IR_DATAGETTER_TESTING_JAR_ деплоится из пайплайна ЦУМ в сандбокс автоматом.
Для прода ресурс _MARKET_IR_DATAGETTER_JAR_ деплоится по кнопке.

Таска _MARKET_IR_DATA_GETTER_, в которой market-ir-datagetetr.jar используются в качестве ресурса, теперь ищет этот ресурс в зависимости от двух параметров:
- _ir_getter_jar_resource_id_ [id ресурса]
- _ir_getter_jar_resource_path_ [resource_type ресурса]

Происходит так: если _ir_getter_jar_resource_id_ > 0, то поиск ресурса происходит по id; по умолчанию -1.
Иначе поиск ведется в списке ресурсов с типом _ir_getter_jar_resource_path_ (например, для [прода](https://sandbox.yandex-team.ru/resources?type=MARKET_IR_DATAGETTER_JAR&limit=20)), где выбирается самый свежий ресурс - с максимальным id.

В настоящий момент на поиск jar по _ir_getter_jar_resource_path_ переведены шедулеры:
- [Matcher Data Getter in stable env](https://sandbox.yandex-team.ru/scheduler/21654/view)
- [Matcher Data Getter in testing env](https://sandbox.yandex-team.ru/scheduler/21670/view)

Старые ненужные ресурсы после нового релиза сейчас нужно удалять вручную (т.к. время хранения - inf) или добавить в пайплайн таску для
чистки старых ресурсов после очередного релиза.


## Сборка и деплой вручную - @deprecated

1. На dev машине, например braavos вызвать:

   ```hs
   arc mount -m ~/arcadia/ -S ~/arc-store/
   cd ~/arcadia/market/ir/ir-datagetter/
   ~/arcadia/ya make
   ~/arcadia/ya upload market-ir-datagetter.jar
   ```

2. Получаем ссылку
   > Download link: https://proxy.sandbox.yandex-team.ru/1707746421

   Нас интересует айдишник в конце 1707746421

3. Заходим под роботом `robot-mrk-ir-dg-prep`.
   Пароль искать тут - https://wiki.yandex-team.ru/market/development/datapreparation/roboty-ir/

4. Заходим на страницу https://sandbox.yandex-team.ru/schedulers?author=robot-mrk-ir-dg-prep и редактируем айдишник на нужный нам  (1707746421) у шедулеров
