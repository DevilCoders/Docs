Пример запуска тестов
```
ya make -tt --test-param=release_version=2019.2.104 --test-param=report_port=17051 --test-param=report_host=report.tst.vs.market.yandex.net --test-tag=ya:not_autocheck --allure=/tmp/allure
```

, где

release_version - версия релиза индексатора, которую мы ожидаем увидеть под репортом

report_host - хост репорта на который будт идти запросы

report_port - порт репорта

allure - путь по которому будет сгенерён allure отчёт

