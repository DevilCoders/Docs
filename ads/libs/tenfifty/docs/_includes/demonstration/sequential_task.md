# Учим catboost поверх последовательного обучения tlm

Учим линейную модель, последовательно двигая скользящее временное окно и применяя очередную полученную модель к данным из будущего, таким образом получаем фичу, которая используется при обучении катбуста.

{% cut "sequential_task.yaml" %}

{% code '/ads/libs/tenfifty/bin/tool/example_tasks/sequential_task.yaml' lang='yaml' lines='taskBegin-taskEnd'  %}

{% endcut %}

{% cut "inner_sequential_task.yml" %}

{% code '/ads/libs/tenfifty/bin/tool/example_tasks/inner_sequential_task.yml' lang='yaml' lines='taskBegin-taskEnd'  %}

{% endcut %}


{% list tabs %}


- Draw

    Команда запуска `./tenfifty_tool ../example_tasks/sequential_task.yaml draw -o graph.html` можно добавить `&& ya upload graph.html` для загрузки в  sandbox

    [Интерактивный граф](https://proxy.sandbox.yandex-team.ru/2556833530)
    ![Картинка графа](pic/seq_task_tlm.jpg)


- Nirvana

    Команда запуска `./tenfifty_tool ../example_tasks/sequential_task.yaml nirvana  --yt_work_dir some_dir`

    [Граф](https://nirvana.yandex-team.ru/flow/eda31730-e2ab-463b-b2f6-864737345618/86221e38-4737-4ce0-b00d-4027d0e86cb4)
    ![Картинка графа](pic/seq_task.jpg)

- Tape

    Команда запуска `./tenfifty_tool ../example_tasks/sequential_task.yaml tape  --yt_work_dir some_dir`


{% endlist %}
