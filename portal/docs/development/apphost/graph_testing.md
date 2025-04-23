## Как тестировать графы

### UI-граф на Хамстере
Графы вертикали MORDA, созданные через UI, можно [посмотреть Horizon](https://horizon.z.yandex-team.ru/graphs?arcpath=UI&vertical=MORDA)
и проверить на хосте хамстера ``https://portal-hamster.yandex.ru``

Чтобы протестировать такой граф, добавьте в запрос cgi-параметр ``graph=`` с префиксом ``testing_``. 

Пример запроса в ПП для UI-графа ``morda_searchapp_degradation``:
```
https://portal-hamster.yandex.ru/portal/api/search/2?graph=testing_morda_searchapp_degradation
```


### Граф на RC


* Коммитим свои изменения в графе в `trunk`. Иного способа пока нет.
* Выкладываем граф в тестинг [по инструкции](https://docs.yandex-team.ru/portal/projects/apphost_release_process).
* Как тестировать:
  * тестинг морды это rc.yandex.ru (rc.yandex.TLD). Запросы в этот балансер попадают в [тестовый аппхост](https://nanny.yandex-team.ru/ui/#/services/catalog/testing-portal-apphost), тестовую морду, тестовые сервисы go.
  * тестинг геохелпера - [l7test.yandex.ru/geohelper](l7test.yandex.ru/geohelper/check).
