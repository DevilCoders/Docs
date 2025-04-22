Позволяет получить перцентили времени закрытия задач для некоторого набора месяцев.

Утилита - бинарный файл.

Позволяет выбрать месяц для начала выборки и конца выборки.

--tasks-filename - файл связи имён и id     
--history-filename - файл истории событий       
--percentiles - список нужных перцентилей в формате '[p1, p2, p3, ..., pn]'     
--wiki-format - вывод в формате таблицы для st.yandex-team.ru       
--from-month, --to-month - начало и конец желаемой выборки, формат MM.YYYY

Для более подробной информации ./generate-mnclose-percentils --help.    
Примеры:    
- ./generate-mnclose-percentils --tasks-filename t_tasks_jule.csv --history-filename mnclose_task_history_full.csv --from-month 01.2019 --to-month 03.2019 --mode STE
: рассчитывает перцентили 50, 90, 99 для выборки с января 2019 по март 2019

- ./generate-mnclose-percentils --tasks-filename t_tasks_jule.csv --history-filename mnclose_task_history_full.csv --tasks-relations-filename t_task_relations.csv --mode ETE:
расчитывает время способами "от конца предков до конца" и "от начала до конца", выводит среднюю разницу в процентах и таблицу данных в вики-формате

- ./generate-mnclose-percentils --tasks-filename t_tasks_jule.csv --history-filename mnclose_task_history_full.csv --tasks-relations-filename t_task_relations.csv --percentiles '[10, 20, 30, 40]' --mode STE
рассчитывает перцентили 10, 20, 30, 40 для времени от начала до конца для максимальной выборки