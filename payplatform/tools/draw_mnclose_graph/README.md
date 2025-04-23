==== Общие параметры
--tasks-filename – файл с описанием вершин, t_tasks.csv, формат <{такой.
"ID","NAME_ID","NAME","TERMINAL_SIGN","TD_SHIFT","TD_DURATION","TD_OVERDUE","IS_ACTIVE","NEED_AUTOOPEN","ALWAYS_STATE_NOTICE","WEIGHT"
402,"t200910_acts_check","Проверить и устранить расхождения в актах",1,691200,172800,0,0,1,0,0
418,"t201010_create_partner_docs","Сформировать документы в OEBS",1,388800,86400,0,0,1,0,0
404,"t200910_shops_acts_create","Выставить акты на Магазинные товары",1,432000,86400,0,0,1,0,0
329,"nt_end","Конечная вершина",0,0,0,0,1,1,0,0
328,"nt_begin","Стартовая вершина",0,0,0,0,1,1,0,0
}>

--tasks-relations-filename – файл с описанием связей между вершинами, t_tasks_relations.csv, формат <{такой.
"TASK_SOURCE_ID","TASK_DESTINATION_ID","TASK_REL_TYPE_ID","TD_SHIFT"
437,441,1,0
421,419,1,0
433,440,1,0
424,440,1,0
}>

--tasks-relations-override-filename – файл с описанием переопределений связей, t_tasks_relations_override.csv, формат <{такой.
"TASK_SOURCE_ID","TASK_DESTINATION_ID","ACTION"
603,527,add
534,527,add
666,527,remove

add - добавление связи, remove - удаление
}>

--tasks-history-filename – файл с историей изменений статуса вершин, t_tasks_history.csv, формат <{такой
"MONTH","ID","NAME","BEGIN_DT","STATE"
01.06.18 00:00:00,864,"ADFox: Генерация актов",01.06.18 00:00:00,"new"
01.06.18 00:00:00,864,"ADFox: Генерация актов",02.06.18 12:11:36,"open"
01.06.18 00:00:00,864,"ADFox: Генерация актов",02.06.18 12:11:42,"resolved"
}>

--result-format – в каком формате выдавать результат: png, svg, html.
--result-filename – имя выходного файла.
==== Параметры для HTML
--template-filename – имя файла с шаблоном, mnclose_graph_template.html.
--cytoscape-filename – имя файла с JS библиотекой Cytoscape, необходимо из-за правок в этой библиотеке, cytoscape.umd.js.
--need-month – данные за какой месяц использовать, в формате 01.06.2019.
--tasks-manual-filename – имя файла со списком ручных вершин, они будут выделены на графе овалами, t_tasks_manual.txt, по одной вершине на строчку, <{например
328
329
}>
==== Использование
Для генерации PNG:
* положить файлы t_tasks.csv и t_tasks_relations.csv рядом с ./run.sh
* запустить run.sh.
Для генерации HTML:
* положить файлы t_tasks.csv, t_tasks_relations.csv, t_tasks_relations_override.csv, t_tasks_history.csv, t_tasks_manual.txt рядом с ./run_html.sh
* исправить в run_html.sh месяц на нужный
* запустить run_html.sh.
