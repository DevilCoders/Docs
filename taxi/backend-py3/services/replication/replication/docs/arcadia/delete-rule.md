## Удаление правила

1. Удалить правила через админку: нужно выбрать группу правил, а затем само
   правило в разделе {{ description_replication_admin }},
   нажать кнопку "Изменить" и в поле "Действие" выбрать ["Удалить состояние"](drafts.md#remove).
   Таким образом удалится очередь и состояние (прогресс) репликации.

2. Если таблицы в YT тоже больше не нужны, есть 2 способа их удалить:
    - Через [админку](drafts.md#yt_remove)
    - [Скриптом](scripts.md#yt_ctl-remove), если вы уже выкатили релиз без правила

3. Удалить yaml-файл правила в директории **dwh/replication_rules**, и, мапперы с тестами,
   если эти мапперы не используются больше ни для каких правил в скоупе.
   После этого выкатить [**replication_rules**]({{ link_to_replication_rules_teamcity }}).
