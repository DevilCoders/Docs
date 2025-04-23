# Последовательное обучение

Представлено композитным действием `RunSequentialTask` (`sequential_task`).

## Параметры

Выполняет последовательный запуск тасок из `parameters->task->graph`

`f"context.after_apply"` - место, куда записать выход одной итерации
`f"context.train"` - место, куда записать вход обучения одной итерации
`f"context.to_apply"` - место, на котором будем предсказывать значения

На вход внутренней на таски для обучения (`f"context.train"`) приходит весь доступной на данном шаге лог. Внутренняя таска, может например воспользоваться GetLastNDays, чтобы выбрать дни для обучения

    start_date: 2021-10-20
    end_date: 2021-10-31 # not included

    days_to_predict: 1 # count of days_predicted per day
    lag_of_train: 1  # lag the last day of train data and first day of prediction

[`start_date`; `end_date`) - в заданном интервале из заданного лога выполняем предсказание

`days_to_predict` - отвечает за то, сколько дней предсказывать за одну итерацию обучения

`lag_of_train` - отступ последнего дня, который подаётся на вход внутренней таске, от первого дня предсказания


Дефолтные значение `days_to_predict=1`, `lag_of_train=1`. Тогда последний день, который будет подан в внутренний таск для обучения, будет на один день отступать от дня предсказания

Вот пример схемы. Train - что подаётся на вход внутренней таске в `f{context.train}`, Predict - `f{context.to_apply}`
![Схема логов](pic/log_schema.png)

## Пример

{% include notitle [sequential_task](../_includes/demonstration/sequential_task.md) %}
