Здоровье маркета 
https://wiki.yandex-team.ru/Market/Development/Health/

Редактирование конфигов переезжает в UI: https://health.market.yandex-team.ru
Подробнее про него тут: https://wiki.yandex-team.ru/Market/Development/Health/Health-UI/

Прежде чем создавать пулл реквест с созданием или правкой конфигов, попробуйте сначала сделать это в UI. Это удобнее и намного быстрее, чем ждать ревью от нас (в котором мы попросим сходить в UI) и потом ждать 4 часа выкладку релииза :)

Собрать всё, запустить юнит-тесты:
```bash
ya make -tAP
```

Запуск интеграционных тестов устарел, так как проверки конфигов проводятся в ui. Если очень нужно запустить, то команда следующая:
```bash
sudo docker-compose -f health-integration-tests/docker/docker-compose.yml up -d
./gradlew :health-integration-tests:integrationTest
```
