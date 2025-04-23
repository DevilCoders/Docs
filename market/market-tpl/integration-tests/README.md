Сборка source'ов без тестов:
```$xslt
ya make
```
Запуск интеграционных тестов:
```$xslt
ya make -ttt
```
Запуск с локальным профилем (нужно сначала запустить локально tpl-int и tpl-api):
```$xslt
ya make -ttt --jvm-args="-Dspring.profiles.active=local-debug"
```
Запуск stress-тестов:
```$xslt
ya make -ttt -F ru.yandex.market.tpl.integration.tests.stress.tests* --jvm-args="-Dstress.tests.enabled=true -Dspring.profiles.active=stress"
```

