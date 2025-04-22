# Отладка и ошибки

### Где лежат логи и можно посмотреть ошибки?

Если проблема воспроизводится, логи можно посмотреть с помощью `cgi`-параметров `?dump=eventlog&eventlog_format=html`, например `https://hamster.yandex.ru/jobs?dump=eventlog&eventlog_format=html`.

Если есть `reqId` запроса, можно воспользоваться [Setrace](https://setrace.yandex-team.ru/ui/).

Посмотреть ошибки можно в `ErrorBooster`: [прод](https://error.yandex-team.ru/projects/apphost/projectDashboard?filter=service%20==%20JOBS%20AND%20additionalKeyValue%20in%20%22ctype%3A%20prod%22), [hamster](https://error.yandex-team.ru/projects/apphost/projectDashboard?filter=service%20==%20JOBS%20AND%20additionalKeyValue%20in%20%22ctype%3A%20hamster%22).

### Где мониторинги и как их править?

Ошибки можно в `ErrorBooster`: [прод](https://error.yandex-team.ru/projects/apphost/projectDashboard?filter=service%20==%20JOBS%20AND%20additionalKeyValue%20in%20%22ctype%3A%20prod%22), [hamster](https://error.yandex-team.ru/projects/apphost/projectDashboard?filter=service%20==%20JOBS%20AND%20additionalKeyValue%20in%20%22ctype%3A%20hamster%22).

Алерты под `ErrorBooster`: [прод](https://juggler.yandex-team.ru/check_details/?host=api.error.yandex-team.ru&service=alert-702&last=1DAY), [hamster](https://juggler.yandex-team.ru/check_details/?host=api.error.yandex-team.ru&service=alert-736&last=1DAY).
Подкручивать [тут](https://error.yandex-team.ru/projects/apphost/settings/alerts?filter=service%20==%20JOBS%20AND%20additionalKeyValue%20in%20%22ctype%3A%20hamster%22).

[Дашборд с ошибками шаблонов](https://yasm.yandex-team.ru/panel/koreil._6Uh7Mg/).

Внизу дашборда два алерта на ошибки шаблонов.

### Алгоритм дебага проблем с КП

???
