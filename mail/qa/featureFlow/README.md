# Сервис контроля за движением фичи

Набор ручек для помощи в ведении проектов

## Чеклисты `/manager/newstatus`
Ручка
Добавляет чеклист в тикет при его переводе в определённый статус.
Если в тикете уже есть чеклист, то он не перезатрётся, пункты добавятся поверх.
Может создавать подзадачи к тикету.

###Параметры
`key` - ключ задачи

`status` - статус, в который перешла задача

### Конфигурация в flow_constants -> status_checklists
Конфиг для добавления чеклиста в тикет.

Формат

```json
{
  '[Очередь]': {
    '[Статус]': [
      '[пункт чеклиста 1]',
      '[пункт чеклиста 2]',
        ...
    ],
      ...
  },
    ...
}
```

### Конфигурация в flow_constants -> status_issues
```json
{
    '[Очередь]': {
        '[Статус]': [
            {
                'type': '[Тип тикета]',
                'summary': '[Заголовок]',
                'description': '[Описание]'
            },
            ...
        ]
    },
    ...
}
```

## Заведение тикета через форму `/dev/issue`
Сама форма https://forms.yandex-team.ru/surveys/98697/ дёргает ручку
и позволяет завести задачу в нужной очереди в соответствии с её правилами.
Правила описываются в конфиге.

### Конфигурация в flow_constants -> dev_issue_params
Формат
```json
    'MAILBACKZBPTEST': { //название очереди
        'sizes_config': { //тип тикета в зависимости от размера проекта
            'L': {
                'type': 'project',
            },
            'M': {
                'type': 'project',
            },
            'S': {
                'type': 'task',
            },
        },
        'service_tag': 'test_services', //тег сервиса, соответствующий id вопроса в форме
        'task_for_each_component': True, //заводить ли отдельную задачу под каждый компонент
        'common_fields': { //дополнительные поля, которые необходимо проставить в каждом тикете
            'assignee': 'a-zoshchuk',
            'components': ['component0']
        },
        'components': { //сервисы или компоненты, существуюищие в очереди, для каждого можно настроить дополнительные поля
            'Тестовый компонент1': {
                'components': ['component11', 'component12'],
                'fixVersions': ['fixVersion11'],
                'tags': ['testTag1']
            },
            'Тестовый компонент2': {
                'components': ['component21', 'component22'],
                'fixVersions': ['fixVersion21'],
                'assignee': 'assignee2',
            }
        }
    },
```

## Призыв формы заведения тикета в коментарии `/manager/make_form`
Можно призвать форму для заведения тикета в комментарий к задаче

###Параметры
`key` - ключ задачи
