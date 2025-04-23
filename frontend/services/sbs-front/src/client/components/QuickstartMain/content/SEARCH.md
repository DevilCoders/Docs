## Что получишь в результате
- [метрики качества](https://wiki.yandex-team.ru/sbs/sbs-metrics/): позапросная доля побед и Bradley-Terry (если включены автоматические ханипоты);
- прокрашивание эксперимента, в случае если система статистически значимо выиграла или проиграла (для каждой пары систем вычисляется значение p-value);
- в случае включённого тегирования СЕРПов, результаты можно фильтровать по [тегу](https://wiki.yandex-team.ru/sbs/manual/search/pluginsfiltersflags/plugins/?from=%2Fsbs%2Fplugins%2F#tegi);
- подробные результаты в формате JSON и TSV для самостоятельного анализа;

## Примеры
1. [Приёмочный офлайн](https://sbs.yandex-team.ru/experiment/93860), сравнение через swap.
2. [Исследование сниппетов](https://sbs.yandex-team.ru/experiment/64855) СЕРПа с использованием плагина.
3. Редизайн просмотрщика картинок [Card-by-Card](https://sbs.yandex-team.ru/experiment/112932) (сниппет).

[Подробнее](https://wiki.yandex-team.ru/sbs/manual/search/) о создании поискового эксперимента и отдельно о [приёмочном SbS](https://wiki.yandex-team.ru/ee/sbs/).
