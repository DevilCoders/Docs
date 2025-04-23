# market-request-utils
Библиотека для упрощения и унификации работы с трассировочными логами.

[Ссылка на страничку в Вики](https://wiki.yandex-team.ru/users/antsa4/requests-tracing/)

[Публикация в Artifactory через ЦУМ](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/market-libraries)


## Использование
Создание записи делается с помощью класса RequestLogRecordBuilder. После заполнения информации о запросе вызовите метод
`build()` и запишите полученную строку в лог.

Пример использования:

```java
RequestLogRecordBuilder record = new RequestLogRecordBuilder();
record.setType(RequestType.OUTPUT);

Triple<Protocol, String, String> split = UrlSplitter.splitUrl(url);

record.setEndTimestampMillis(CLOCK.millis());
record.setDurationMillis(duration);
record.setRequestId(marketRequestId);
record.setTarget(Module.BLACKBOX);
record.setRetryNumber(1);
record.setErrorMessage(error);
record.setProtocol(split.getLeft());
record.setTargetHost(split.getMiddle());
record.setQuery(split.getRight());
record.setHttpMethod(HttpMethod.GET);
record.setHttpCode(status);

String message = record.build();

LOGGER.log(message);
```
