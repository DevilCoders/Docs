# Учим catboost поверх tlm с CrossLearning

Учим линейные модели в CrossLearning, предсказания моделей на тестовых фолдах формируют фичу, которая используется при обучении катбуста.
Другая линейна модель учится на всем датасете, переданном в CrossLearning, и используется в предсказаниях катбуста.

{% cut "crosslearning_task.yaml" %}

{% code '/ads/libs/tenfifty/bin/tool/example_tasks/crosslearning_task.yaml' lang='yaml' lines='taskBegin-taskEnd'  %}

{% endcut %}

{% cut "inner_crosslearning_task.yml" %}

{% code '/ads/libs/tenfifty/bin/tool/example_tasks/inner_crosslearning_task.yml' lang='yaml' lines='taskBegin-taskEnd'  %}

{% endcut %}


{% list tabs %}


- Draw

    Команда запуска `./tenfifty_tool ../example_tasks/crosslearning_task.yaml draw -o graph.html` можно добавить `&& ya upload graph.html` для загрузки в  sandbox

    [Интерактивный граф](https://proxy.sandbox.yandex-team.ru/3108474746)
    ![Картинка графа](pic/crosslearning_task_draw.jpg)


- Nirvana

    Команда запуска `./tenfifty_tool ../example_tasks/crosslearning_task.yaml nirvana  --yt_work_dir some_dir`

    [Граф](https://nirvana.yandex-team.ru/flow/6f3d274f-a6f6-4cfc-a28f-b0f202e2f0e5/793a0397-e8d8-4a36-ad71-05b9107e0a5c)
    ![Картинка графа](pic/crosslearning_task.jpg)

- Tape

    Команда запуска `./tenfifty_tool ../example_tasks/crosslearning_task.yaml tape  --yt_work_dir some_dir`


{% endlist %}
