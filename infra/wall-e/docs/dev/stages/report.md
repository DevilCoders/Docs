# Startrek Report Stage

Стейдж создаёт тикет на починку проблемы, о которой сигнализирует загоревшаяся проверка. В будущем этот стейдж станет заменой статусу dead и будет использоваться для сигнализации о проблемах с обработкой других стейджей (сейчас эти проблемы собираются в ежедневные отчёты, как и хосты в статусе dead, но этот процесс имеет определённые недостатки и неудобства).

Стейдж использует механизм отчётов. По сути, каждый хост/задача имеет либо собственный отчёт, однако если понадобится, то можно сделать, чтобы задача подключалась к общему отчёту, в зависимости от ситуации. Если отчёты отключены в настройках проекта – стейдж всё равно создаёт тикет с теми настройками, которые указаны – выключение отчётов приводит к отключению ежедневных отчётов, а не этих тикетов.

## Flowchart
[Оригинальный документ](https://jing.yandex-team.ru/files/n-malakhov/Startrek%20Stage.xml), можно импортировать в [draw-io](https://drawio.yandex-team.ru) и отредактировать (не забудьте перевыложить).

{% list tabs %}

- SVG

  ![flowchart](../../_assets/startrek_stage_flowchart.svg)

- PNG

  ![flowchart](../../_assets/startrek_stage_flowchart.png)

{% endlist %}

## Control Flow
[Оригинальный документ](https://jing.yandex-team.ru/files/n-malakhov/Startrek%20Stage%20Control%20Flow.xml), можно импортировать в [draw-io](https://drawio.yandex-team.ru) и отредактировать (не забудьте перевыложить).

{% list tabs %}

- SVG

  ![control flow chart](../../_assets/startrek_stage_control_flow.svg)

- PNG

  ![control flow chart](../../_assets/startrek_stage_control_flow.png)

{% endlist %}
