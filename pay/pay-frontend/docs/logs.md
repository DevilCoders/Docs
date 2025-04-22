# Логи

## Логи в YT

- [Аккаунт в YT](https://yt.yandex-team.ru/hahn/accounts/general?filter=logfeller-yande&account=logfeller-yandex-pay-web)

### Production

- [access-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/yandex-pay-web-payments-access-log)
- [duffman-access-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/yandex-pay-web-payments-duffman-access-log)
- [duffman-http-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/yandex-pay-web-payments-duffman-http-log)


### Testing

- [testing-access-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/yandex-pay-web-payments-testing-access-log)
- [testing-duffman-access-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/yandex-pay-web-payments-testing-duffman-access-log)
- [testing-duffman-http-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/yandex-pay-web-payments-testing-duffman-http-log)


## Logbroker

- [yandex-pay/frontend](https://lb.yandex-team.ru/logbroker/accounts/yandex-pay/frontend)


## Мониторинги

- [График потребления квоты](https://solomon.yandex-team.ru/?project=yt&cluster=hahn&service=accounts&l.account=logfeller-yandex-pay-web&l.sensor=node_count*&graph=auto&stack=false&b=7d)
- [Алерты на квоту в Solomon](https://solomon.yandex-team.ru/admin/projects/yandex-pay-web/alerts)


## Конфиги для Logfeller

- [yandex_pay_web_project.json](https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/yandex_pay_web_project.json)
- [yandex_pay_web_hahn_logs.json](https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/yandex_pay_web_hahn_logs.json)
- [yandex_pay_web_hahn_streams.json](https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/yandex_pay_web_hahn_streams.json)


## Формула и пример расчёта квоты на ноды в YT

Текущая нагрузка рассчитывается по формуле — `c * Σ(aᵢ/bᵢ)` , где `a` — время жизни таблицы, `b` — периодичность лога и `c` — количество топиков.

У нас есть 6 топиков и 3 типа логов — однодневный, тридцатиминутный и пятиминутный. Однодневные хранятся 60 дней, тридцатиминутные — 7 дней и пятиминутные — 1 день.

Итого нам необходимо:
```
((60 / 1) + ((7 * 24 * 60) / 30) + ((24 * 60) / 5)) * 6 = 4104 ноды
```
Для тридцатиминутных и пятиминутных логов расчёты произведены в минутах.
