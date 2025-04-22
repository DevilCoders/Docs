# html

Генератор HTML-отчетов о покрытии.

Основан на [istanbul html-report](https://github.com/istanbuljs/istanbuljs/tree/master/packages/istanbul-reports/lib/html).

Отличия:
- учитывается только покрытие функций (без учета колонок),
- суммарное покрытие строк рассчитывается по покрытию функций.
