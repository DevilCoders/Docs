# Логирование

Для логирования используется фреймворк [**log4j2**](http://logging.apache.org/log4j/2.x/manual/)

## Как работает
**Конфиг:** https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/mbi-billing/src/main/conf/log4j2.xml

Для того чтобы логировать какую-либо информацию необходимо создать логер с помощью фабрики (импортируем логгер slf4j)
```
private static final Logger LOG = LoggerFactory.getLogger(SomeClass.class);
```
И далее с помощью `LOG.logging-level(message)` происходит логирование.

### Уровни логирования
* TRACE
* DEBUG
* INFO
* WARN
* ERROR
* FATAL

## Рекомендация по изменению логов

1. Открыть [XdocSupplyBillingExecutor](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/mbi-billing/src/java/ru/yandex/market/billing/fulfillment/billing/xdoc/XdocSupplyBillingExecutor.java)
1. Создать логер
   ```
   private static final Logger LOG = LoggerFactory.getLogger(XdocSupplyBillingExecutor.class);
   ```
1. Добавить логирование в Job-у XdocSupplyBillingExecutor
    ```
    LOG.info("!!! LOG IS CHANGED !!!");
    ```
1. Запустить tms(займет некоторое время, подробнее: [Запуск tms локально](https://docs.yandex-team.ru/market-billing/guide/basics/local-tms)) и выполнить джобу XdocSupplyBillingExecutor
    ```
    nc 127.0.0.1 13713
    tms-run xdocSupplyBillingExecutor
    ```
1. Найти изменения в mbi-billing.log (~/arcadia/market/mbi/mbi/logs), например через cat mbi-billing.log | grep "LOG IS CHANGED"
