# ExpFlags

## Конвертация флагов в эксперименты

### Ошибка `Testid "flag=value" has an empty config. Check that the flag exists in the storage.`

Пример полного текста ошибки:

```
Not all test-ids have been created!
Testid "yandex_login=yalogin (fiji-21429)" has an empty config. Check that the flag exists in the storage.
```

> 📖 Это временная ошибка, которая в корне будет исправлена после FEI-17530 и связана с [разделением хэндлера REPORT](https://wiki.yandex-team.ru/serp/experiments/docs/report-webvideoimg/#moegoflaganetvnovomxendlere). Хэндлер `REPORT` признан устаревшим и не учитывается инструментами.

Ошибка сигнализирует о том, что эксперимент, который инструмент собирается завести в AB, имеет пустой конфиг. Как правило это связано с тем, что в [хранилище флагов AB](https://ab.yandex-team.ru/flag_storage/flag) нет флага для актуальных хэндлеров сервиса. Других известных причин пока нет, но они могут быть.

Проверить, что проблема именно в том, что отсутствует флаг с актуальным хэндлером в хранилище флагов, можно следующим образом:

1. Из лога получаем название флага.
2. Делаем запрос из браузера: `https://ab.yandex-team.ru/api/v1/flag_storage/flag?search=<flag_name>`.
3. Если в ответе есть только одна запись с хэндлером `REPORT`, то это та проблема. В противном случае что-то не так — лучше сходить в infraduty.

Существует два варианта решения проблемы с отсутствием флага с актуальным хэндлером:

1. Вручную создать флаг с таким именем и нужным для вашего сервиса хэндлером из интерфейса AB.
2. Положить флаг в код сервиса согласно [регламенту](https://wiki.yandex-team.ru/search-interfaces/infra/infraspeed/docs/expflags/expflags-regulations).
