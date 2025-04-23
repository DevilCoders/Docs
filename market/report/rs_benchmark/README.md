## Бенчмарк для отладки производительности базового поиска Репорта в связке с Remote Storage.

1. Собрать зависимости:
```
ya make -r market/report/rs_benchmark
```

2. Скачать и распаковать архивы с индексом, патронами и RS индексом (опционально):
```
wget https://proxy.sandbox.yandex-team.ru/2192814734 -O - | market/report/rs_benchmark/uc -t ~/rs_benchmark_data/ -d -x
wget https://proxy.sandbox.yandex-team.ru/2115381904 -O - | market/report/rs_benchmark/uc -t ~/rs_benchmark_data/ammo/ -d -x
wget https://proxy.sandbox.yandex-team.ru/2192883886 -O - | market/report/rs_benchmark/uc -t ~/rs_benchmark_data/ -d -x
```

3. Подготовить среду и запустить Репорт и RS:
```
ya make -r market/report/report_base
market/report/rs_benchmark/rs_benchmark.py start --index ~/rs_benchmark_data
```

4. Прогнать тест производительности:
```
market/report/rs_benchmark/rs_benchmark.py test --ammo-file ~/rs_benchmark_data/ammo/market_base_white_offer_ammo.txt [--request-count 100000] [--cache-limit 0.5]
```

5. Если результат получается нестабильным то можно попробовать запустить репорт с привязкой к NUMA-ноде:
```
market/report/rs_benchmark/rs_benchmark.py start --index ~/rs_benchmark_data --numa-bind
```
Опционально остановить фоновые процессы (может быть опасно):
```
market/report/rs_benchmark/rs_benchmark.py suspend_tasks
```
Прогнать стрельбу в один поток с пятикратным повторением:
```
market/report/rs_benchmark/rs_benchmark.py test --ammo-file ~/rs_benchmark_data/ammo/market_base_white_offer_ammo.txt --request-count 1000 --stream-count 1 --repeat 5
```

6. Чтобы снять снапшот индекса надо на первой машине мини-кластера выполнить:
```
pkill -STOP instancectl
pkill -STOP reanimator
pkill backctld
pkill access-agent
pkill report
tar chf - data/clickdaemon.keys pdata/access-agent/state pdata/access-agent/install data/search/rty_index -C data/search dynamic_models fast_data_outlets formulas fulfillment index lms loyalty marketdynamic promo_secondaries qbid-mds qpromos report-data vendor_model_bids_cutoff vendor_offer_bids_cutoff | bin/uc -c -C lzma-0 -t /tmp/index.tar.lzma
pkill -CONT reanimator
pkill -CONT instancectl
ya upload --skynet --ttl 365 --owner <user> --token <token from https://sandbox.yandex-team.ru/oauth> /tmp/index.tar.lzma
```
