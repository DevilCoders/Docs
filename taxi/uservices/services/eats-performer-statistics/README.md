## eats-performer-statistics

### Описание
Сервис рассчитывает статистические данные по исполнителям заказов (курьерам/сборщикам) и далее отдает их в мобильное приложение для отображения.

### Назначение 
Агрегация и отображения исполнителям заказов статистики об их работе

---

### Полезности
Добавление новой метрики
  1. Добавить в **src/utils/pull_metrics/yql_requests** запросы в _**YT**_ для метрик по аналогии с остальными
  2. Добавить в **src/utils/pull_metrics/requests_builder.cpp** в функцию
       **_CreateYQLRequests_** новую метрику по аналогии с остальными
  3. Выкатить изменения
  4. Добавить в **eats_performer_statistics_statistics_params**(конфиг3.0) метрику
         * Добавить описание метрики в **metrics_intervals**
         * Добавить сбор метрики в **periodic_ids**
