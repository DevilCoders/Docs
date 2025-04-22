### calc_errors_budget_exceeded

1. Найди проблемные акции при помощи запроса: https://yql.yandex-team.ru/Operations/YsazY5fFt1Qna7JUHapHCPGTp193V4io3WRy0hr-0SA=

2. Сообщи авторам акций о проблеме/договорись об отключении акций. Как найти автора: https://st.yandex-team.ru/PROMOGUIDE-23

Тикет на разработку: https://st.yandex-team.ru/MARKETDISCOUNT-7261

### total_percentage_alert

1. Смотрим график: https://monitoring.yandex-team.ru/projects/market-loyalty/explorer/queries?q.0.text=let%20total_usage%20%3D%20group_by_labels%28%7Bcluster%3D%22stable%22%2C%20environment%3D%22PRODUCTION%22%2C%20http_method%3D%22calc%22%2C%20object_type%3D%22coin%7Ccoupon%7Cpromocode%22%2C%20period%3D%22five_min%22%2C%20project%3D%22market-loyalty%22%2C%20sensor%3D%22coin-total-usages%22%2C%20service%3D%22back%22%7D%2C%20%27sensor%27%2C%20v%20-%3E%20group_lines%28%27sum%27%2C%20v%29%29%3B%0Alet%20errors%20%3D%20group_by_labels%28%7Bcluster%3D%22stable%22%2C%20environment%3D%22PRODUCTION%22%2C%20error_type%3D%22%2A%22%2C%20http_method%3D%22calc%22%2C%20object_type%3D%22coin%7Ccoupon%7Cpromocode%22%2C%20period%3D%22five_min%22%2C%20project%3D%22market-loyalty%22%2C%20sensor%3D%22coin-error-total-usages%22%2C%20service%3D%22back%22%7D%2C%20%27sensor%27%2C%20v%20-%3E%20group_lines%28%27sum%27%2C%20v%29%29%3B%0Alet%20percentage%20%3D%20%28errors%20%2F%20total_usage%29%20%2A%20100%3B%0A%0Apercentage&from=now-3h&to=now&utm_source=solomon_view_metrics&refresh=60000&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg

2. Если массовые ошибки с ручкой `calc`, причины могут быть разные:
- факап loyalty
- парсеры/фродеры

Разбираем совместо с дежурными https://abc.yandex-team.ru/services/marketpromo/duty2/30744 

3. Если по графику в самом алерте % не превышал 50, то создать тикет в MONSUPPORT с просьбой прокомментировать причину срабатывания алерта. (возможно, недоезд метрик лоялти в моменте)

4. Если недоезд, нужно создать задачу в st/PROMOMONITORING и поставить исполнителем @nickshevr
