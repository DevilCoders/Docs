# IR-b2b - тестирование Matcher, Clutcher, Formalizer, Skutcher

## Запуск качественных тестов
Запуск тестов отдельных компонентов: _matcher.Main_, _clutcher.Main_, _formalizer.Main_, _skutcher.Main_.

Пример запуска _matcher.Main_ для сравнения работы двух сборок матчера с VM options:
```sh
-Db2b_tests.yt.token="YOUR_TOKEN"
-Dinput.hdfs.directory="//home/market/production/ir/sc/stratocaster/recent/offers"
-Dmatcher.stable.host="http://iva1-4149-235-iva-market-test-m-f87-9855.gencfg-c.yandex.net:9855/"
-Dmatcher.testing.host="http://sas2-1744-bf9-sas-market-test--51a-10886.gencfg-c.yandex.net:10886/"
-Dmatcher.offer.batch.size="256"
-Dmatcher.offer.batch.count="24"
```
В тесте качественно сравнивается работа стабильная и тестовая сборки Матчера при опросах ручки
```sh
/MatchBatch
```
Результаты теста записываются в файлы по умолчанию (можно изменить в VM options):
```sh
full-report.json
overview-report.html
```

## Подготовка файлов для нагрузочного тестирования Matcher через Tank по ручке /MatchBatch
Запуск _matcher.stress_tests.Main_ с VM Options:
```sh
-Db2b_tests.yt.token="YOUR_TOKEN"
-Dinput.hdfs.directory="//home/market/production/ir/sc/stratocaster/recent/offers"
-Dmatcher.testing.host.uri="sas2-1744-bf9-sas-market-test--51a-10886.gencfg-c.yandex.net:10886"
-Dmatcher.offer.batch.size="256"
-Dmatcher.offer.batch.count="24"
-Drequests.tank.ammo.file.name="requests_tank_ammo_file"
-Drequests.protobuf.example.file.name="requests_protobuf_example"
```

Все POST запросы /MatchBatch записываются в файл патронов в формате _requests-style_ c protobuf внутри, пригодный для нагрузочного тестирования одного тестового матчера через ya.Tank:
```sh
requests_tank_ammo_file
```

Для первого POST запроса формируется protobuf файл, который можно использовать для опроса тестового Матчера в ручном режиме (например, через _Postman_).
```sh
requests_protobuf_example
```