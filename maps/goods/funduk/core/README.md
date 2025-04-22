**Обязательные переменные для операций:**
- environment - production или test
- jar_path - путь на YT до jar файла 

**Обязательные переменные для задачника:**
- tasker_workdir - путь на YT до папки с таблицами задачника
- tasker_projects_path - путь внутри проекта (вида /ru/yandex/...json) до файла с конфигурацией проектов

**Операции для товарного поиска:**
- update_configs - обновление таблиц со словарями
- export_base_builder - построение экспорта товарного поиска
  - ypath - путь до папки на YT, где будет построена база (входные данные должны лежать там же)
- provider_updater - обновление данных от поставщиков
- price_decode_preprocessor - нарезка картинок для расшифровки в толоке
- photo_loader - прокачка фотографий, собранных в шаблонах PRICE_DECODE_YANG, PRICE_DECODE_YANG_CHAIN (работает только на homer)
- tagging_train - построение датасета для обучения формулы тегов
  - ypath - папка для результатов 
  - tagging_rubric - рубрика для тегов
- tagging_apply - построение датасета для применения формулы тегов
  - ypath - папка, где отработала джоба tagging_train
  - tagging_rubric - рубрика для тегов
- tagging_apply_formula - применение формулы к датасету из tagging_apply
  - ypath - папка, где отработала джоба tagging_apply и есть формула model.bin

**Операции для задачника:**
- task_waiter - ожидание синхронизации
- queue - сформировать очередь для проекта
  - tasker_project - код проекта
  - [tasker_queue_query] - если true, то только вывести запрос для формирования очереди без его исполнения
- send_in_work - отправить задачи в очереди в работу
  - tasker_project - код проекта
  - tasker_exportdir - папка на YT для выгрузки данных
  - [tasker_query_condition] - дополнительное условие на задачи, которые отправить в работу
- execute_custom_query - выполнить кастомный запрос проекта (CustomQuery queries)
  - tasker_project - код проекта
  - tasker_query_to_execute - имя запроса в конфигурации проекта

**Другие операции:**
- yql - выполнение YQL запроса
  - текст запроса берется из текствого входа операции

**How to run**

%%(bash)
export yt_token=$(cat ~/.yt/token)
export yql_token=$(cat ~/.yql/token)

job_id=update_configs env=testing ./run.sh ru.yandex.assay.funduk.Main
%%
