# Миграция на версию 4

Версии 2 и 3 были почти полностью совместимы. Ломающих изменений не было.

В версии 4 обратная совместимость впервые нарушена достаточно сильно, чтобы повлечь неожиданные эффекты.

Важные изменения:

  * User Agent больше не отправляется по умолчанию в `vars`, в переменной `1042`, это необходимо включить опцией `sendClientUa`
  * Счётчик `tech.perf.external_resource` удалён, так как он дублирует `tech.perf.traffic`
  * Счётчик `tech.perf.static.location` удалён, так как эти данные отправляются во всех остальных счётчиках в поле `-cdn`
  * Метод `Ya.Rum.sendFirstPaint` удалён, так как он был deprecated с версии 2.0
  * Метрика `before_bem-init` спрятана за опцию `sendBeforeBemInited`
  * Переменная `13` (URL) в `sendResTiming` спрятана за опцию `sendUrlInResTiming`
  * Отправка автоматически размеченных ресурсов (`data-rcid`) спрятана за опцию `sendAutoResTiming`
  * В методе `sendRaf` отправка первого rAF спрятана за опцию `sendFirstRaf`
  * Автоматическая отправка Element Timing спрятана за опцией `sendAutoElementTiming`
  * Опция `forceFirstPaintTimeSending` переименована в `forcePaintTimeSending`, так как отвечает на самом деле за все отрисовки
  * RUM больше не отправляет параметры `dtype=stred, pid=1, cid=72202`, потому что никто не помнит, зачем они нужны
  * Опция `crossOrigin` удалена вместе с автоматическим подключением скрипта nearest.js, теперь его нужно подключать руками, если нужна информация о CDN
  * LCP больше не отправляется, если в процессе загрузки менялась видимость страницы

Для максимальной совместимости с версией 3 нужно задать в начале следующие настройки:

```js
Ya.Rum.init({
    sendClientUa: true,
    sendBeforeBemInited: true,
    sendUrlInResTiming: true,
    sendAutoResTiming: true,
    sendAutoElementTiming: true,
    sendFirstRaf: true,
    forcePaintTimeSending: old.forceFirstPaintTimeSending // Важно! Опция переименована!
});
```

Но включать по умолчанию отправку всех полей не рекомендуется, так как это тратит дисковое пространство
и замедляет парсинг логов. Рекомендуется спрятать их за экспериментальным флагом.
