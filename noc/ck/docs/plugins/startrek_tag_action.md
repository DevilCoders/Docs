# startrek_tag - получить или изменить теги startrek-задачи

## Параметры

- `issue` - задача в startrek; если не указано, то используется startrek-задача, с которой был
  создан job
- `name` - тег или список тегов, которые должны быть добавлены или удалены к startrek-задаче; можно
  не указывать теги, что может быть полезно для простого получения тегов задачи
- `state` - состояние тега (тегов), которое должно быть обеспечено: `present` - будут добавлены
  теги, если их нет, `absent` - будут удалены теги, если их нет; по-умолчанию `present`

## Возвращаемое значение

Возвращает список тегов, которые были у задачи после изменения тегов

## Примеры

```yaml
- name: Установить тег noc:dev к задаче NOCREQUESTS-33760
  startrek_tag:
    issue: NOCREQUESTS-33760
    name: noc:dev
    state: present

- name: Установить теги noc:dev и experts_line к задаче NOCREQUESTS-33760
  startrek_tag:
    issue: NOCREQUESTS-33760
    name:
        - noc:dev
        - experts_line
    state: present

- name: Удалить тег nocduty_line из задачи NOCREQUESTS-33760
  startrek_tag:
    issue: NOCREQUESTS-33760
    name: nocduty_line
    state: absent

# в переменную current_issue_tags будет записан список тегов:
# ["experts_line", "heat", "noc:dev", "noc:dev:ops+mon+fw+puncher", "noc:other"]
- name: Получить теги задачи, с которой был создан текущий job
  startrek_tag:
  register: current_issue_tags
```
