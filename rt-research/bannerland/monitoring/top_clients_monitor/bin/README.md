# Мониторинг топ клиентов

Запуск:
```bash
ya make -r && ./top_clients_monitor_bin
```

Необходимо предоставить следующие токены через переменные окружения: `YT_TOKEN`, `YQL_TOKEN` (эти два можно ваши) и `SOLOMON_TOKEN` (для него нужно брать https://yav.yandex-team.ru/secret/sec-01fvmcbqen683frer1j81t2bgn/explore/versions).

При запуске автоматически выбирается `release_type = testing`, и результат пишется в testing таблички и метрики пушатся в testing кластер в соломоне. Продакшен не трогается вообще.
* [Тестовые таблички](https://yt.yandex-team.ru/hahn/navigation?path=//home/bannerland/testing/monitorings/top_clients)
* [Тестовые графики](https://monitoring.yandex-team.ru/projects/bannerland/explorer/queries?q.0.s=%7Bproject%3D%22bannerland%22%2C%20cluster%3D%22testing%22%2C%20service%3D%22top_clients%22%2C%20sensor%3D%22top_clients_stat.cost%22%2C%20banners_type%3D%22perf%22%7D&utm_source=solomon_shard_graphs&range=1d&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg)
