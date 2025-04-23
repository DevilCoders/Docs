# pers-static

### Описание 

Показ отзывов пользователей на "Большом маркете"

[Страница на Wiki](https://wiki.yandex-team.ru/market/development/pers/grade/static/)

[API (swagger)](http://pers-static.tst.vs.market.yandex.net:34522/api/swagger-ui.html)

### Выкладка

[Релиз из транка](https://tsum.yandex-team.ru/pipe/projects/pers/delivery-dashboard/pers-static-arc)

[Выкладка в тестинг из ветки](https://tsum.yandex-team.ru/pipe/projects/pers/release/new/pers-static-branch)

### RTC

[Nanny](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_static/)

Логи в ```logs/pers-pay/pers-pay.log```

Секретница:
- [тест](https://yav.yandex-team.ru/secret/sec-01f33raq7v13sbs5bkma2ve9gg/explore/versions)
- [прод](https://yav.yandex-team.ru/secret/sec-01f33rbppypdcfhf0jpj3np755/explore/versions)

После изменения секрета можно накатить его через `persec static test/prod`

### Графики

[Solomon](https://solomon.yandex-team.ru/admin/projects/market-pers-static)

[Основные метрики pers-static](https://grafana.yandex-team.ru/d/000001656/pers-static)

[nginx прода](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketpersstatic;ctype=production;prj=market/)

[proto метрики прода](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketpersstatic;ctype=production;prj=market/?range=21660000)

[Метрики saas](https://saas-mon.n.yandex-team.ru/monitor/?ctype=stable&service=market-pers-static&kind=proxy&dc=&allserv=)

[Метрики saas по машинкам](https://yasm.yandex-team.ru/chart/signals=%7Bquant~saas_unistat-times-stable-market-pers-static_dhhh~50,quant~saas_unistat-times-stable-market-pers-static_dhhh~90,quant~saas_unistat-times-stable-market-pers-static_dhhh~95,quant~saas_unistat-times-stable-market-pers-static_dhhh~97,quant~saas_unistat-times-stable-market-pers-static_dhhh~98,quant~saas_unistat-times-stable-market-pers-static_dhhh~99,quant~saas_unistat-times-stable-market-pers-static_dhhh~999,const~120,const~100%7D;hosts=ASEARCH;itype=searchproxy/?top_method=maxavg&top_signal=quant(saas_unistat-times-stable-market-pers-static_dhhh%2C50)&range=21600000)

[proto метрики тестинга](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketpersstatic;ctype=testing;prj=market/?range=21660000)

### Таблицы с документами

[production](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Fmarket%2Fproduction%2Fpers-grade%2Ftables%2Fsaas_documents)

[testing](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Fmarket%2Ftesting%2Fpers-grade%2Ftables%2Fsaas_documents)

### Ferryman

[production](http://market-pers-static-stable.ferryman.n.yandex-team.ru/get-namespaces?hr=1)

[testing](http://market-pers-static.ferryman.n.yandex-team.ru/get-namespaces?hr=1)


### Сборка и запуск 

Сборка и прогон тестов `ya make -tt`

Локальный запуск можно сделать напрямую и через скрипт. Подробности в [документации](https://wiki.yandex-team.ru/users/ilyakis/maret-java-arcadia-migration/#lokalnyjjzapusk)

[Локальный сваггер](http://localhost:8080/api/swagger-ui.html)

#### Локальный запуск через скрипт
Запуск приложения
```
# простой запуск
./local-start.sh

# в режиме отладки
./local-start.sh --debug-port=6666
```

#### Локальный запуск напрямую
Локальный запуск - через класс `ru.yandex.market.grade.statica.PersStaticMain`
Переменные окружения
```
ENVIRONMENT=local
```

JMV args
```
# если хочется, чтобы логи выводились в консоль
-Dlog4j.configurationFile=/home/#USER/arc/arcadia/market/pers/static/src/main/conf/local/log4j2-test.xml
```


