Сверка с id {{ run.id }} успешно завершилась.
Время работы: {{ run.work_time }} ({{run.started}} {{run.finished}})
{% if run.diffs_count_yt > run.diffs_count_limit %}Найдено расхождений (всего): {{run.diffs_count_yt}}

**Внимание! Лимит расхождений был превышен. В БД загружено только первые {{run.diffs_count_limit}} расхождений.**
{% else %}Найдено расхождений (всего): {{run.diffs_count}}

Статистика уникальных расхождений:
{% for dict in run.diffs_stat %}{{ dict.type_str }}: {{ dict.total }}
{% endfor %}{% endif %}
Результаты запуска: {{ run.current_diffs_ui_url }}
