# @yandex-int/dx-metrics-logger 1.2.0

## Минорные изменения

Добавлена опция `useMilliseconds` - принимает `true` или `false` (по-умолчанию `false`)
Если передать эту опцию в кнструктор в значении `true`, тогда все тайминги будут измеряться в миллисекундах.
Если не передавать опцию либо передать `false` - тайминги как и прежде будут измеряться в секундах.

| Заголовок                                                         | Задача                                   | PR        |
| :---------------------------------------------------------------- | :--------------------------------------- | :-------- |
| feat(dx-metrics-logger): Добавлена опция логгирования в мс        | [https://st.yandex-team.ru/TURBOUI-6612] | [1628874] |
| feat(dx-metrics-logger): Метод logMetric теперь возвращает промис | [https://st.yandex-team.ru/TURBOUI-6612] | [1628874] |

## Пояснения

[TURBOUI-6612]: https://st.yandex-team.ru/TURBOUI-6612
[1628874]: https://a.yandex-team.ru/review/1628874/details