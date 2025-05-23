# Объекты управления

Большинство [команд](commands-groups.md) `sky` выполняется на удаленных серверах ([хостах](glossary.md#host)) или в [porto-контейнерах](glossary.md#container). Обязательным аргументом таких команд является список хостов, на которых необходимо выполнить команду.

Множество объектов, на которых необходимо выполнить команду, может быть задано перечислением. Но в большинстве случаев команды выполняются на группе объектов, объединенных по определенному признаку (например, множество хостов, относящихся к [группе инстансов](glossary.md#instance-group)).

Для гибкого выбора хостов или прочих объектов, на которых должна быть выполнена команда, поддерживаются два формата указания:

#### Калькулятор Блинова

Стандартный синтаксис описания для операций над множествами хостов или инстансов сервисов. Подробное описание см.  документе [Калькулятор Блинова](https://doc.yandex-team.ru/generated/skynet/sky/blinovcalc.html).

#### Устаревший синтаксис

Устаревший синтаксис используется для реализации обратной совместимости. С помощью него можно указывать только хосты.

Поддерживаются процедуры объединения («+») и исключения («-»).

Хосты, которые необходимо включить в результаты, задаются со знаком плюс (`+`). Например: `+wstest02`.

Формат определяется автоматически при выполнении команды. Недопустимо одновременное использование обоих форматов в рамках одной команды.

При указании хостов могут использоваться [диапазоны значений](#range-of-values) (поддерживаются средствами bash).


## Диапазон значений {#range-of-values}

Для сокращенного указания серверов, на которых необходимо выполнять команды, а также для уменьшения вывода могут быть использованы диапазоны значений. Работа с диапазонами обеспечивается стандартными средствами bash. Например, следующая конструкция соответствует всему множеству хостов с префиксом «ws8-»: `ws8-{00..99}`.

> Рассмотрим следующую конструкцию:
> 
> ```
> +wstest{01..99}
> ```
> 
> После обработки указанного диапазона (`wstest{01..99}`) средствами bash конструкция принимает следующий вид:
> 
> ```
> +wstest01 +wstest02 ... +wstest99
> ```

При использовании [калькулятора Блинова](https://doc.yandex-team.ru/generated/skynet/sky/blinovcalc.html) перед выполнением команды проверяется наличие всех указанных хостов (если не используется специальный ключ `--dont_check_hosts` — не выполнять проверку хостов в DNS).  Если не найден по крайней мере один хост, полученный в результате вычисления диапазонов, команда не выполняется.

> Рассмотрим следующую конструкцию:
> 
> ```
> h@wstest{01..99}
> ```
> 
> {% include [range-of-values-bash-process](_includes/targets-classif/id-range-of-values/bash-process.md) %}
> 
> 
> ```
> h@wstest01 h@wstest02 ... h@wstest99
> ```

