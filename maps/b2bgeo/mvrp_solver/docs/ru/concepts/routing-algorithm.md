# Алгоритм маршрутизации

## Что оптимизируется

Общая стоимость равна стоимости решения с учетом штрафов. Система выбирает вариант решения с минимальной общей стоимостью, в ответе от API это поле `total_cost_with_penalty`.

Стоимость решения `total_cost` формируется из стоимости используемых транспортных средств (подробнее об этом в разделе [Стоимость автомобиля или курьера](properties-of-vehicles.md#stoimost-avtomobilia-ili-kurera)).

По конкретному транспортному средству стоимость рассчитывается следующим образом:

<hr>
`cost.fixed`  + (<количество рейсов> * `cost.run` )+ (<суммарный пробег по всем рейсам> * `cost.km`)+ (<суммарное время работы по всем рейсам> * `cost.hour`) + (<суммарное количество выполненных заказов> * `cost.location`)
<hr>

Для большинства ситуаций эта формула отражает структуру реальных затрат на маршрут: есть какая-то фиксированная стоимость использования машины (`cost.fixed` и/или `cost.run`) и есть переменная составляющая, которая зависит от пробега/времени/количества заказов (`cost.km`/`cost.hour`/`cost.location` соответственно). На практике чаще всего используются `cost.fixed`, `cost.km` и `cost.hour`, они и содержат определенные значения по умолчанию.

Таким образом, алгоритм минимизирует значение `total_cost_with_penalty` (сумма стоимости решения `total_cost` и штрафов `total_penalty`).

Все стоимости должны быть сбалансированы между собой: размер штрафов относительно стоимости машин, размеры штрафов относительно друг друга. Иначе результаты планирования могут получаться не совсем ожидаемыми. Значения стоимостей и штрафов, заданные по умолчанию, позволяют получать хорошие результаты, но часто их требуется модифицировать под конкретную задачу.

## Некоторые особенности работы алгоритма

С точки зрения практического использования алгоритм обладает следующими свойствами:

- вероятностный подход к решению задачи. Такой подход позволяет гарантировать хорошее качество решения на абсолютно любых задачах по маршрутизации. На практике это означает, что на одном и том же наборе исходных данных результат планирования может быть различным. Но, как правило, по метрике `total_cost_with_penalty` эти решения отличаются друг от друга незначительно.

- наличие жестких и мягких ограничений.

- предсказуемое время работы алгоритма – подробнее об этом в разделе [Время обработки запроса](request-processing-time.md).

## Общая структура стоимости и штрафов

Общая структура стоимости и штрафов изображена на [схеме](https://courier.yandex.ru/vrs-doc/solver-costs.png). Более детальная информация о том, как формируются штрафы, приведена в разделе [Подробнее о штрафах](more-about-penalties.md).



<p class="p"><a href="feedback.html" class="xref button">Написать в службу поддержки</a></p>
