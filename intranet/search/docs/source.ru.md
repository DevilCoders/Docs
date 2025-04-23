# Добавление нового источника

## Что надо сделать для добавления источника
- Решить, должен ли данный источник быть кусочком вертикали "Всё" или нет. Если да, то ничего делать не нужно. Если нет, то нужно добавить новый сервис в https://ssm.n.yandex-team.ru. Эту форму нужно заполнить дважды, один раз для тестинга (вкладка prestable), один раз для продакшена (stable). В качестве способа поставки данных нужно выбрать logbroker (PQ). Остальные параметры можно уточнить у команды SaaS.

- Нужно добавить настройки `endpoint api` для источника (файл `settings.app_settings.isearch.yaml`, внутри yaml файла `api.<source_name>`).

- Добавить scope в настройки (файл `settings.app_settings.isearch.yaml`, внутри yaml файла `scopes.<scope_name>`). `scope_name должно иметь суффикс search`

- Нужно создать класс для запросов к api в `core/sources/<source_name>`.

- Добавить класс `Source`, наследующий `core.swarm.indexer.Indexer` или `core.swarm.api_indexer.PagedApiIndexer`, в `core/sources/<source_name>`.

- Класс Source должен возвращать класс `Snippet`, который надо реализовать в `core/snippets`. В сниппете должны лежать все отображаемые поля, то есть все поля, которые необходимы для отображения документа в выдаче.
- Класс Source должен уметь возвращать тело документа в функции do_create. Тело документа должно содержать всю необходимую *текстовую* информацию. Важно: если по некоторым полям должен осуществляться поиск, но они не должны попадать в пассажи, эти поля следует поместить в зону `z_ns_hidden` (или в зону `!hidden`, зона с таким названием будет автоматически переименована в зону `z_{названиепоиска}_hidden`). Пассажи – это кусочки документа, которые будут подсвечены при выдаче сниппета. Важно: нужно обязательно указать зону `z_ns_hidden` в файле `rtyserver.diff-{имяпоиска}` в настройках вашего SaaS-сервиса (например, https://saas-mon.n.yandex-team.ru/service_info?service=intrasearch_so&ctype=stable).

- Добавить фасеты в метод `emit_attrs` и в настройки в `scopes.<scope_name>.facets`.

- Добавить факторы в метод `emit_factors`.

- Нужно сделать четыре миграции в `core/migrations`: добавить `Revision`, `Service`, `permission` и выдать для `permission` полный доступ (примеры `0007_stackoverflow_add_service_and_revision.py` и `0008_stackoverflow_permission.py`). Лучше всего, чтобы все четыре миграции были в одном файле.

- Если хочется, чтобы заработали оценки, нужно сделать еще одну миграцию (`0015_moebius_marks_and_suggestedanswer.py`), добавив в `choices` название новой вертикали, и настроить оценки для новой вертикали в админке (см. конец инструкции)

- Нужно добавить настройки для `SaaS` (файл `settings/app_settings/isearch.yaml` в `api.saas.<saas_service_name>`). С высокой вероятностью `indexer` должен будет наследовтаь `api.saas_abstract.base.indexer`. Чтобы узнать точно нужно посмотреть `logbroker_host` `SaaS` сервиса. Также, возможно, потребуется посмотреть настройки `SaaS push client`, которые находятся в файле `settings/app_settings/default.yaml` в `saas_push_client`. `path` и `pruning` можно оставить пустыми.

- Нужно добавить правило для источника и для его колдунщика в файл `abovemeta/decider/rules/isearch_rules.py`.

- В файл `setting/celery/global_config/isearch.py` нужно добавить cron таски на реиндексацию источника.

- Добавить факторы в `Saas`, как описано в инструкции в `docs/factors.md`.

- Добавить ревизию по [ссылке](https://search-back.test.yandex-team.ru/_admin/sources/<source_name>/default/revisions?organization_id=).

- Задать в настройках `rtyserver.diff` настройку `"PruneAttrSort":"formula:pruning_rank"`. Это нужно для того, чтобы заработал прунинг. В настройках в файле `relev.conf-{имясервиса}` нужно:
  1. В разделе `dynamic_factors` нужно указать динамические факторы. Можно скопировать этот блок из `intrasearch_so`.
  2. В разделе `static_factors` нужно указать те факторы, которые мы эмитим. Каждый фактор должен быть в формате `"STAT_{имяпоиска}_{имяфактора}": {"index": индекс по порядку, "default_value": 0}`
  3. В разделе `formulas` нужно добавить два ключа.
  4. Первый ключ - `pruning_rank` содержит в себе ещё один ключ, `polynom`. Это полином прунинга, и он должен быть достаточно простым. Скомпилированный полином может быть получен из обычного с помощью ссылки на конвертор полиномов: https://saas-mon.n.yandex-team.ru/polynom_converter?service={имя_вашего_саас_сервиса}. Самый простой прунинг-полином может выглядеть например так: `1*STAT_stackoverflow_updated`.
  5. Второй ключ: `default`. Он может называться и иначе, но проще всего назвать `default`. Это формула ранжирования. В этом разделе может быть два ключа. Один называется `matrixnet`, другой называется `polynom`. Ключ matrixnet указывает на машинно-обученную FML-формулу, например так: `"matrixnet": "fml-844944.info-intrasearch_so"`. Чтобы это сработало нужно не забыть скопировать формулу из fml. Чтобы это сделать, нужно нажать на кнопку fml-copy... и выбрать в качестве `Fml formula id` номер текстовой формулы из fml (например, 844944). В качестве `File name` можно указать fml-{id}, например fml-844944. После нажатия формула будет скачана в вашу рабочую директорию, а к имени файла будет приписано окончание `.info-{имясаассервиса}`. Имя этого файла и нужно указать в ключе `matrixnet`. Второй ключ - `polynom`, позволяет использовать matrixnet-формулу в качестве одного из параметров полинома. Важно: чтобы это заработало, в `dynamic_factors` обязательно должен быть ключ с именем `MatrixNet`. Полином здесь генерируется с помощью того же генератора полиномов, что и в случае прунинга, но стоит сделать его более хитрым. Например, для stackoverflow это `1*MatrixNet+0.3*STAT_stackoverflow_updated+0.5*STAT_stackoverflow_is_answered`.
  6. Нужно не забыть добавить в админке формулу. Сделать это нужно дважды: в тестинге https://search-back.test.yandex-team.ru/_admin/formula/viewer/ и в продакшене https://search-back.yandex-team.ru/_admin/formula/viewer/. Для этого нужно выбрать ваш поиск и ваш SaaS-cервис, в поле "готовый полином" нужно написать `default`. Больше делать ничего не нужно.
  7. Нужно раскатить изменения в SaaS-конфигах: https://saas-mon.n.yandex-team.ru/deploy?service=intrasearch_so&ctype=prestable (подставьте в параметрах ваш SaaS-сервис и prestable/stable в зависимости от того, тестинг это или продакшен). Нужно отжать галочку "only save" и нажать "Deploy".

- Если хочется, чтобы заработали оценки, надо  **после** выкатки кода добавить в админке название вертикали в `enable_marks`. В админке это находится по ссылке https://search-back.test.yandex-team.ru/_admin/features/group/yandex/

## Возможные ошибки и сложные места

- Не работает `SaaS push client`.

Нужно подключиться к нему с помощью `ya tool gdb`

```bash
supervisorctl stop saas_push
ya tool gdb /intrasearch/etc/bin/saas-push
run -c /intrasearch/etc/saas/saas_push.conf
```

Затем почитать ошибку и понять, что не так.

- Не появляется выдача.

Почитать ошибки по [ссылке](https://saas-mon.n.yandex-team.ru/export_errors?service=<saas_service_name>&ctype=prestable).

- Индексация зацикливается.

Это означает, что скорее всего вылетает исключение, которое не получается обработать и которое неунаследовано от `RecoverableError` или `UnrecoverableError`.
Должно помочь наследование этого исключения.


## Полезные ссылки

- Получить [выдачу](https://search.test.yandex-team.ru/<scope_name>?text=hello&plainjson=1) в формате json.
- Посмотреть напрямую [ответ](https://search-back.test.yandex-team.ru/_abovemeta/?text=hello&scope=<scope_name>) от бэкенда с нужным scope.
