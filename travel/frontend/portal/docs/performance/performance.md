# Производительность портала

Раздел про скорость работы портала. Под скоростью работы подразумевается скорость отображения страниц и отзывчивость интерфейса при взаимодействии пользователя с ним.

## Инструменты

-   [Мониторинг релизов](releaseMonitoring.md)
-   [Замер страниц](releaseMonitoring.md)
-   [Сравнение стендов](compareStands.md)

## Метрики

Результат замера страницы с помощью Lighthouse

-   `score` - Общая оценка. [Подробней](https://web.dev/performance-scoring/)
-   `fcp` (First Contentful Paint) - Время отображения хоть какого-то контента. [Подробней](https://web.dev/i18n/ru/first-contentful-paint/)
-   `lcp` (Largest Contentful Paint) - Время отображения самого большого элемента на экране. [Подробней](https://web.dev/lighthouse-largest-contentful-paint/)
-   `speedIndex` - Время, отражающее, как быстро отображается контент на странице во время загрузки. [Подробней](https://web.dev/i18n/ru/speed-index/)
-   `tti` (Time To Interactive) - Время до момента, когда пользователь может нормально взаимодействовать со страницей. [Подробней](https://web.dev/i18n/ru/interactive/)
-   `tbt` (Total Blocking Time) - Общее время блокировки основного потока долгими задачами (сверх 50мс). Т.е. если задача длится 70мс, то в tbt учтется только 20мс. [Подробней](https://web.dev/i18n/ru/lighthouse-total-blocking-time/)
-   `cls` (Cumulative Layout Shift) - Общий сдвиг макета. [Подробней](https://web.dev/i18n/ru/cls/)
-   `maxPotentialFid` - Максимально возможное время ожидания пользователя при первом взаимодействии со страницей. [Подробней](https://web.dev/lighthouse-max-potential-fid/)
-   `ttfb` (Time To First Byte) - Время до первого байта. [Подробней](https://web.dev/i18n/ru/time-to-first-byte/)
-   `mainThreadWork` - Общая продолжительность работы в основном потоке. [Подробней](https://web.dev/i18n/ru/mainthread-work-breakdown/)
-   `jsExecutionTime` - Общее время выполнения скриптов. [Подробней](https://web.dev/bootup-time/)
-   `domSize` - Количество элементов в документе. [Подробней](https://web.dev/i18n/ru/dom-size/)
