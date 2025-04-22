Быстрый тест обвязки сервиса вычисления моделей, от поступления http-запроса
до входов модели и от выходов модели до отдачи http-ответа.

Запускает сервис над фейковой моделью, единственная нода которой сериализует
все пришедшие входы, делает выходной эмбеддинг из получившегося json
и выходной фактор из хэша получившегося json. Дальше проверяет, что ответ
в правильном формате, извлекает json из эмбеддинга, проверяет, что значение
фактора ему соответствует, и пишет json-ы на канонизируемый выход.

Создание модели: ```
touch emptyfile
quality/relev_tools/bert_models/models_tool/models_tool -o pseudo_model.htxt -f emptyfile -c pseudo_model.proto.txt --storage-uniq-id pseudo_model
```

Запросы генерируются тем же методом, что и для тестов models_proxy,
search/daemons/models_proxy/tests/generator, с дополнительными параметрами,
чтобы сервис вообще запрашивался с возможно большим набором данных на входе,
и ограничением в 10 запросов (держать много запросов здесь не имеет смысла,
с учётом 150+ документов в каждом запросе; так весь тест работает
комфортное для ручного запуска время ~10s).
Патч в generator/__main__.py: ```python
            query += '&rearr=cfg_models=pseudo_model:test,debug'
            query += '&rearr=scheme_Local/ModelsProxy/FetchMainContentUrl=1'
            query += '&rearr=scheme_Local/ModelsProxy/FetchZones=1'
            query += '&rearr=scheme_Local/ModelsProxy/PassAllExpansions=1'
```
Запросы в CFG_MODELS выдираются через `sed 's/.*CFG_MODELS:request=\([^\t]*\).*/\1/' subsources.tskv | gzip > cfg_models_sample.txt.gz`.
