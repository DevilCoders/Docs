# hourglass_thread_pool_usage


## Описание { #description }
Алерт на уровень утилизации тред-пула в Jobs. Задачи (демоны, джобы) запускаются в пуле фиксированного размера.
Когда задач оказывается больше, чем способен вместить пул — какая-то их часть не сможет быть запущена.

**Если проверка горит дольше 10 минут — будет заведен SPI.**

## Диагностика { #diagnostics }
Посмотреть график общего и числа занятых тредов (ссылка есть в тексте juggler-события).
На нем будет две линии:
- hourglass_running – число тредов, в которых прямо сейчас выполняются задачи
- hourglass_threads — общий размер тред-пула

Возможные варианты:
- естественный рост числа задач (на протяжении недель/месяцев)
- выпало из работы большое число хостов
- выкатили новый релиз с необычным ростом нагрузки

## Решение { #solution }
Алерт может зажигаться в WARN при учениях/регламентных работах/выпадении ДЦ — это нормально, делать ничего не нужно.  
Если все хосты в работе, а алерт желтый — при выпадении ДЦ мы можем "не вытянуть" нагрузку.
Следует иметь ввиду этот факт (например отменять собственные учения).

Нужно добавить ресуров (одним из способов):
- добавить подов (одинаковое число в каждом ДЦ)
- оценить утилизацию ресурсов ([пример тикета](https://st.yandex-team.ru/DIRECT-122430)) и увеличить размер тред-пула в конфиге

В качестве временной меры можно попробовать подкрутить порог в коде алерта или поставить даунтайм.


## Ссылки { #links }
- [код алерта в solo](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/jobs/hourglass_utilization.py)
- пример [тикета на увлечиние тредпула](https://st.yandex-team.ru/DIRECT-122430)
