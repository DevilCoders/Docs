## Examples
### Download batch
```(bash)
echo '[{"per-query-parameters":{"query-text":"Кира Найтли"},"serp-request-id":"1"}]' | ./download_batch.py --searchengine yandex-baobab --parse
```
[doc](https://wiki.yandex-team.ru/qe/scraper/api/#acinxronnoezadanienabatchevujuskachkuzaprosov)

[authorization](https://wiki.yandex-team.ru/JandeksPoisk/Metrics/API/#avtorizacija)
### Download single serp
```(bash)
./download_single_serp.py --searchengine google-web --host https://google.ru --summary
```
### Fetch query group
```bash
python3 fetch_qg.py 1004 -l 1 -r | python3 try_prepare_custom.py --config-file 2gis-cat.json
```

### Start metrics experiment

[doc](https://wiki.yandex-team.ru/jandekspoisk/metrics/API/experiments/)
```bash
cat example_experiment_parameters.json | ./start_experiment.py --owner <your-login>
```

On dev:
```bash
cat dev_example_experiment_parameters.json | ./start_experiment.py --owner <your-login> --experiments-url 'https://metrics-experiments-dev.metrics.yandex-team.ru/'
```

### Diff urls from soy
```
./url_diff.py (cat baobab1 | jq -r .uri) (cat islands1 | jq -r .uri )
```


### Build curl
Builds curl for serp.

1. Download single serp json from metrics ([wiki](https://wiki.yandex-team.ru/JandeksPoisk/Metrics/compare/#json))
2. `./build_curl.py serp.json --metrics`
