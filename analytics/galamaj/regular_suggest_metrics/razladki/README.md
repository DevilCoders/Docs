
Странички с текущими worker и launcher для разладок проетка https://razladki.yandex-team.ru/api/suggest_metrics_avrg_time_per_symbol/config/view/worker https://razladki.yandex-team.ru/api/suggest_metrics_avrg_time_per_symbol/config/view/launcher

Загрузить worker curl -F file=@suggest_metrics_worker.conf http://razladki.yandex-team.ru/api/suggest_metrics_avrg_time_per_symbol/config/put/worker

Загрузить launcher curl -F file=@suggest_metrics_launcher.conf http://razladki.yandex-team.ru/api/suggest_metrics_avrg_time_per_symbol/config/put/launcher

Страничка с запусками пересчета разладок https://razladki.yandex-team.ru/suggest_metrics_avrg_time_per_symbol/monitoring

Страничка с всеми разладками https://razladki.yandex-team.ru/api/suggest_metrics_avrg_time_per_symbol/events_history?all=true&as_txt=True&unique_statuses=True

подписать пользователя на разладки  curl -X POST -d @suggest_metrics_notifications.conf "http://razladki.yandex-team.ru/admin/api/set_subscription" --header "Content-Type:application/json"

Полностью пересчитать все разладки за время, начиная с таймштампа. Полезно, если меняем настройки разладок curl "http://launcher.razladki.yandex-team.ru/recalc/suggest_metrics_avrg_time_per_symbol" -d '{"ts_from": 1488326400}'

Уведомления можно настроить так https://wiki.yandex-team.ru/Razladki/DizDok/api/#primerdobavlenijapodpiski По умолчанию "queue": "default" и это означает присылай письмо как только увидел разладку, то есть каждую минуту. Посмотреть другие варианты здесь: https://wiki.yandex-team.ru/Razladki/DizDok/api/#upravleniepodpiskami
