Инструмент позволяет строить визуализации графов FCM и MnClose с учётом связей между ними.
Работает с файлами .csv дампами баз данных FCM и MnClose.
Чтобы работать с данными MnClose нужно указать:

--mnclose-tasks-filename (t_tasks)

--mnclose-relations-filename (t_tasks_relations)

--mnclose-history-filename(t_tasks_history)

Для работы с FCM ужно указать

--fcm-relations-filename

--fcm-history-filename

Для построения объединённой визуализации кроме всего вышесказанного нужно указать .json файл со связями между графами:

--cross-relations-filename.

Чтобы на выходе получить диаграмму Гантта, указать

--gantt-template-filename (gantt_template.html)

--gantt-output-filename (writeable)

Чтобы на выходе получить визуализацию графа, указать

--graph-template-filename (graph_template.html)

--graph-output-filename (writeable)

Можно получать диаграмму и визуализацию как вместе, так и по отдельности.