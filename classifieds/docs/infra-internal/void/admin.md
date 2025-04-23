
## Администрирование через  drills-helper
Для упрощенного администрирования shiva можно использовать приложение [drills-helper](https://docs.yandex-team.ru/classifieds-ops-internal/duty/drills-helper#ustanovka).

### Управление деплоем

Синтаксис команды:
```bash
drills-helper deploy disable shiva -l <layer> -d <dc> # Отключение деплоя

drills-helper deploy enable shiva -l <layer> -d <dc> # Включение деплоя
```
где: `<layer>` - имя слоя (test/prod), `<dc>` - имя датоцентра (vla/sas).  
Более подробно об управлении деплоем можно прочитать в [Документации drills-halper](https://docs.yandex-team.ru/classifieds-ops-internal/duty/drills-helper#upravlenie-deploem).

## Текущее состояние деплоя shiva

Текущее состояние деплоя можно определить по дашборду [Drills overview](https://grafana.vertis.yandex-team.ru/d/I1-gRG8Zk/drills-overview?orgId=1&refresh=1m) в разделе `Admin services status`.
- [SAS](https://grafana.vertis.yandex-team.ru/d/I1-gRG8Zk/drills-overview?orgId=1&refresh=1m&viewPanel=48)
- [VLA](https://grafana.vertis.yandex-team.ru/d/I1-gRG8Zk/drills-overview?orgId=1&refresh=1m&viewPanel=47)


## Администрирование через API
Для администрирования shiva существует grpc-апи, находящееся по адресу `` shiva-admin.vertis.yandex.net:443 `` для shiva в prod и `` shiva-admin.test.vertis.yandex.net:443 `` для shiva в test. Для работы с реальными сервисами необходимо использовать апи продовой шивы с указанием слоя в команде, в то время как через тестовую шиву в основном выкатываются наши тестовые сервисы. Для авторизации нужен oauth-токен, который можно получить  [здесь](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=1f82008746cd4bcfb3e2679e747974f9), для запроса из консоли можно использовать grpcurl.

### Список методов
#### Работа с флагами
Общее апи для работы с глобальными флагами сервиса, на данный момент поддерживаются следующие флаги:
- TestSasOff
- TestMytOff
- ProdSasOff
- ProdMytOff
- TestYdSasOff
- TestYdVlaOff
- ProdYdSasOff
- ProdYdVlaOff

Данные флаги отвечают за выключение деплоя в соответствующих слое и дц. При попытке размещения в недоступном дц пользователям будем показано сообщения вида "Сервис деплоя временно недоступен. Причина - reason"

При учениях в одном дц следует закрывать только этот дц, например для myt это делается командой
```
grpcurl -d '{"list":[{"name":"ProdMytOff", "reason":"тут я напишу причину выключенного дц и приложу ссылку на тикет"}]}' -H "authorization: Bearer $TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.SetFlags
```

А для sas
```
grpcurl -d '{"list":[{"name":"ProdSasOff", "reason":"тут я напишу причину выключенного дц и приложу ссылку на тикет"}, {"name":"ProdYdSasOff", "reason":"учения"}]}' -H "authorization: Bearer $TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.SetFlags
```

Для открытия дц надо вызвать метод ClearFlags с теми же флагами, причина при очистке флага будет проигнорирована

Т.е. для myt
```
grpcurl -d '{"list":[{"name":"ProdMytOff"}]}' -H "authorization: Bearer $TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.ClearFlags
```

а для sas -
```
grpcurl -d '{"list":[{"name":"ProdSasOff"}, {"name":"ProdYdSasOff"}]}' -H "authorization: Bearer $TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.ClearFlags
```

При факапах может понадобиться полностью закрыть деплой в прод, это можно сделать с помощью команды ``` grpcurl -d '{"list":[{"name":"ProdMytOff", "reason":"тут я напишу причину выключенного дц и приложу ссылку на тикет"}, {"name":"ProdSasOff", "reason":"тут я напишу причину выключенного дц и приложу ссылку на тикет"}, {"name":"ProdYdSasOff", "reason":"тут я напишу причину выключенного дц и приложу ссылку на тикет"}, {"name":"ProdYdVlaOff", "reason":"тут я напишу причину выключенного дц и приложу ссылку на тикет"}]}' -H "authorization: Bearer $TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.SetFlags ```
\
&nbsp;

#### GetFlags
Возвращает все установленные флаги
Аргументы: отсутствуют

При успехе возвращает список флагов и причин их установки, при ошибке - ошибку.
Пример запроса:
```
grpcurl -H "authorization: Bearer $TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.GetFlags
```

#### SetFlags
Устанавливает флаги с указанием причины
Аргументы:
* list - список флагов, представленных в виде названия (name) и причины (reason)

При успехе возвращает пустой ответ, при ошибке - ошибку.
Пример запроса:
```
grpcurl -d '{"list":[{"name":"ProdMytOff", "reason":"учения"}]}' -H "authorization: Bearer $TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.SetFlags
```
Пример запроса, отключающего деплой в весь прод:
```
grpcurl -d '{"list":[{"name":"ProdMytOff", "reason":"тут я напишу причину выключенного дц и приложу ссылку на тикет"}, {"name":"ProdSasOff", "reason":"тут я напишу причину выключенного дц и приложу ссылку на тикет"}, {"name":"ProdYdSasOff", "reason":"тут я напишу причину выключенного дц и приложу ссылку на тикет"}, {"name":"ProdYdVlaOff", "reason":"тут я напишу причину выключенного дц и приложу ссылку на тикет"}]}' -H "authorization: Bearer $TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.SetFlags
```
#### ClearFlags
Отключает флаги
Аргументы:
* list - список флагов, представленных в виде названия (name) и причины (reason). Причина в данном запросе игнорируется

При успехе возвращает пустой ответ, при ошибке - ошибку.
Пример запроса:
```
grpcurl -d '{"list":[{"name":"TestMytOff"}]}' -H "authorization: Bearer $TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.ClearFlags
```

#### BulkDeployment
Массовый перезапуск сервисов, задеплоенных через shiva. Запустить несколько параллельных балк рестартов нельзя.

Аргументы:
* layer - слой, 1 для test и 2 для prod
* issue - номер тикета
* comment - комментарий к деплою, который увидят пользователи, если подписаны на изменения своего сервиса. Например - "обновление версии лог драйвера"
* issue - номер задачи в рамках которой происходит деплой сервисов
* services - список сервисов, которые будут перезапущены. Для каждого сервиса также будут перезапущены бранчи в этом слое.
* actualConfiguration - флаг, отвечающий за конфигурацию с которой будут перезапущены сервисы.
  Если false - берется конфигурация как у последнего запущенного приложения, дополняя актуальными сгенерированными переменными, версией лог драйвера и т.д.
  Если true (небезопасно) - берется самая актуальная конфигурация (карта, манифест, базовые переменные окружения)
* all - флаг, отвечающий за перезапуск всех сервисов в слое.

При успехе возвращает id, по которому можно узнать состояние деплоймента, при ошибке - ошибку.
Пример запроса:
```
grpcurl -d '{"layer":1, "comment":"обновление версии лог драйвера", "issue": "ISSUE-100", "services":["service1", "service2"], "actualConfiguration":false}' -H "authorization: Bearer $TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.BulkDeployment
```

#### BulkDeploymentState

Возвращает состояние балк деплоймента, включающее в себя статистику по состояниям и список неперезапущенных сервисов
Аргументы:
* id - id балк деплоймента. Необязательный аргумент, при его отсутствии будет возвращенно состояние последнего (то есть текущего).


При ошибке возвращает ошибку, а при успехе объект, содержащий следующие поля:
* id - id балк деплоймента
* login - логин инициатора
* layer - слой (1 для test, 2 для prod)
* comment - комментарий к перезапуску
* notStarted - количество еще не перезапущенных сервисов
* started - количество сервисов, которые перезапускаются в данный момент
* canceled - количество сервисов, перезапуск которых был отменен (возможна отмена как при отмене балк деплоймента, так и при ручной отмене перезапуска владельцем сервиса, второй вариант отразится в описании)
* success - количество сервисов, которые были успешно перезапущены
* failed - количество сервисов, которые не смогли перезапуститься
* failedServices - массив, содержащий объекты, описывающие проблемные сервисы, содержащий следующие поля:
    * name - название сервиса
    * branch - ветка, в которой был запущен сервис
    * reason - причина неудачного перезапуска
* canceledServices - массив, аналогичный failedServices, но для отмененных перезапусков

Пример запроса:
```
grpcurl -d '{"id":1}' -H "authorization: Bearer $TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.BulkDeploymentState
```

#### CancelBulkDeployment

Отменяет текущий bulk deployment. Не отменит происходящие в данный момент деплойменты и не откатит уже презапущенные сервисы.
Аргументы:
* id - id балк рестарта. Необязательный аргумент, при его отсутствии будет отменен последний (то есть текущий).


При успехе возвращает пустой ответ, при ошибке - ошибку.
Пример запроса:
```
grpcurl -d '{"id":1}' -H "authorization: Bearer $TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.CancelBulkDeployment
```
