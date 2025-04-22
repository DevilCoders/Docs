===Что это

travel/avia/shared_flights/tasks/flying_time/bin/flying_time - это скрипт, выгружающий минимальное время прямого
перелёта между городами на ближайшие 330 дней.

Пример локального запуска
```(sh)
 export AVIA_PGAAS_PASSWORD=<see https://yav.yandex-team.ru/secret/sec-01e84cae2rjpe3pvwjrt9c0phb>
./bin/flying-time --environment=testing --records_limit=100 --output_mode=text --output_file=a.txt
```
