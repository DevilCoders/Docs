### Описание

Клиент для [Tарифницы](https://st.yandex-team.ru/MARKETMONEY-324). Использует авторизацию TVM

### Как использовать
1. Подключить библиотеку к себе в проект. В `ya.make` в секцию `PEERDIR` добавить `market/billing/tariffs/mbi-tariffs-client`
2. Импортировать спринговый конфиг [ru.yandex.market.mbi.tariffs.client.TariffClientConfiguration](https://a.yandex-team.ru/arc_vcs/market/billing/tariffs/mbi-tariffs-client/src/main/java/ru/yandex/market/mbi/tariffs/client/TariffClientConfiguration.java#L35)
```
@Import(TariffClientConfiguration.class)
```
3. Создать бин `TariffTvm2ClientProperties`
4. Добавить необходимые проперти:
```
# путь до балансера тарифницы.
mbi.tariffs.balancer.path=
#    Прод: https://mbi-tariffs.vs.market.yandex.net
#    Тест: https://mbi-tariffs.tst.vs.market.yandex.net

# Нужно или нет писать логи для запросов из клиента. По дефолту - false
mbi.tariffs.debug.requests=
```

5. TVM идентификаторы тарифницы (заполнить надо в бине `TariffTvm2ClientProperties`)
```
Прод: 2024863
Тест: 2024861
```

