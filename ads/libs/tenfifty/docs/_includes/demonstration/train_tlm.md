# Учим tlm

Обучаем линейную модель с помощью [tlm](https://wiki.yandex-team.ru/users/stepych/tlm/).

{% cut "train_tlm.yaml" %}

{% code '/ads/libs/tenfifty/bin/tool/example_tasks/train_tlm.yaml' lang='yaml' lines='taskBegin-taskEnd'  %}

{% endcut %}

{% list tabs %}


- Draw

    Команда запуска `./tenfifty_tool ../example_tasks/train_tlm.yaml draw -o graph.html` можно добавить `&& ya upload graph.html` для загрузки в  sandbox

    [Интерактивный граф](https://proxy.sandbox.yandex-team.ru/2560017859)
    ![Картинка графа](pic/tlm_demo.jpg)


- Nirvana

    Команда запуска `./tenfifty_tool ../example_tasks/train_tlm.yaml nirvana  --yt_work_dir some_dir`

    [Граф](https://nirvana.yandex-team.ru/flow/05748248-3008-4403-9ce1-cc9e42002afa/8ed563ca-041f-4972-b9dc-7a3e728a22d6)
    ![Картинка графа](pic/tlm_nirvana.jpg)


- Tape

    Команда запуска `./tenfifty_tool ../example_tasks/train_tlm.yaml tape  --yt_work_dir some_dir`


{% endlist %}
