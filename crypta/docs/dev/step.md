## Оркестрация через STEP

Позволяет запускать Sandbox-задачи по триггеру или связывать их выполнение между собой.

Документация: <https://wiki.yandex-team.ru/sandbox/step>  
Документация API: <https://wiki.yandex-team.ru/statbox/infrastructure/doc/api/#events>  
API: <https://step.sandbox.yandex-team.ru/api/v1/events>  
UI: <https://step-ui.qloud.yandex-team.ru/configs>

Через API в систему отправляются **events** с набором параметров.
При возникновении определенного события могут запускаться **actions** - таски sandbox с набором парамеров.
То, какие **actions** срабатывают после каких **event** - определяется с помощью конфигурации **action configs**.

Смотреть и изменять конфигурацию action configs можно через UI и через API.
Взаимодействовать с events можно только через API.
Как проверять срабатывание actions - я не понял :)

### Использование в Крипте
Все luigi и Sandbox задачи Склейки репортят свой статус в STEP через прослойку в виде Crypta API([task/status](https://api.crypta.yandex-team.ru/swagger/index.html#/task/reportNewTaskStatus)).
Статус задачи репортится как event **cryptaTaskEvent** с параметрами *taskType*, *taskStatus*, *environment* и др.

Actions configs для продакшн процессов задаётся через код в [crypta/graph/orchestration/step](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/orchestration/step).
Их можно посмотреть в [UI](https://step-ui.qloud.yandex-team.ru/configs/?author=robot-crypta).

### Как создать новый action config
1. Добавить новую конфигурацию по аналогии с существующими в `crypta/graph/orchestration/step/action_configs.py`
2. Взять sandbox токен robot-crypta в [секретнице](https://yav.yandex-team.ru)
3. Собрать и запустить 
```bash  
ya make  
export SANDBOX_TOKEN=<robot-crypta sandbox token>  
./action_configs  
```
4. Будет выведен статус, что обновилось.

*Note: название конфига не всегда соответсвует названию таски. Это нужно, чтобы запускать один тип таски с разными параметрами.*

### Как проверить, что нужные event появляются
Только через [STEP API](https://step.sandbox.yandex-team.ru/api/v1/events):
```bash
curl "https://step.sandbox.yandex-team.ru/api/v1/events?name=cryptaTaskEvent&params__taskType=CRYPTA_GRAPH_HUMAN_MATCHING_YAML&sort=-_id&limit=2" | jq
```

### Как проверить, сработал ли action при появлении event и создалась ли  sandbox задача с нужными параметрами
```bash
# Получаем id нужных событий
curl "https://step.sandbox.yandex-team.ru/api/v1/events?name=cryptaTaskEvent&params__taskType=CRYPTA_GRAPH_HUMAN_MATCHING_YAML&sort=-_id&limit=2" | jq '.result[]._id'
event_id = 'YOUR_EVENT_ID'
# Получаем event history id
curl -X POST "https://step.sandbox.yandex-team.ru/api/v1/event_story" -d "id=$event_id" | jq '.id'
event_history_id='YOUR_EVENT_HISTORY_ID'
# Получаем номера запущенных sandbox задач
curl "https://step.sandbox.yandex-team.ru/api/v1/event_story/$event_history_id" | jq '.result.produced_tasks[].sandbox_task_id'
# 
```
В ответах из API есть и другие полезные данные для отладки


### Как зарепортить статус таски вручную
Можно через Swagger в Crypta API, который отправит событие в STEP.
Пример, история таски `CRYPTA_GRAPH_PREPARE_SOUP_YAML`:
1. Зайти на <https://api.crypta.yandex-team.ru/swagger/index.html#/task/reportNewTaskStatus>
2. Заполнить параметры и запустить
```
taskType=CRYPTA_GRAPH_PREPARE_SOUP_YAML`
taskStatus=SUCCESS`
environment=stable`
body={'date': '2019-01-01'}`
```

### More
<https://wiki.yandex-team.ru/crypta/matching/internal/devops/orkestracija-zadach>  
[CRYPTR-522](https://st.yandex-team.ru/CRYPTR-522)  
[CRYPTR-505](https://st.yandex-team.ru/CRYPTR-505)  