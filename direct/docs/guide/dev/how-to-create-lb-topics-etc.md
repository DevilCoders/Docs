# Создание топиков/консьюмеров и других штук в LogBroker 

## Создать новый топик

### Коротко

1. Напиши json-описание топика в https://a.yandex-team.ru/arc/trunk/arcadia/direct/schemata/logbroker  
1. Поревьюй названия/параметры топиков (у кого? Для начала — как код)
1. Закоммить json-ы в транк. Тикет в коммите — обычный DIRECT
1. Сгенерируй команды для создания топика. Для этого зайди на `ppcdev`, в [примонтированном репозитории Аркадии](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#mount) в каталог `direct/schemata/logbroker`, и запусти  ```./create-topic.py $path_to_topic.json```, где `$path_to_topic.json` - путь к json-файлу с описанием топика. Пример готовой команды:  
```./create-topic.py lbkx/direct/direct-ppcdict-binlog-log-json-query.topic.json```  
Команда выведет stdout несколько команд с программой logbroker, сохрани их.
1. Напиши вручную тикет DIRECTMIGR "создать топики по таким-то json-ам", укажи в нем путь к топику как в примере, и добавь в тикет команды для создания топика, сохраненные выше. Пример <https://st.yandex-team.ru/DIRECTMIGR-1793>
1. Напиши в админский чат или дежурному app-duty тикет DIRECTMIGR и "создайте топики пожалуйста"
1. Инструкция для app-duty: [link](../jeri/lb-create-objects.md)

### Подробности

Описания живут [в репозитории](https://a.yandex-team.ru/arc/trunk/arcadia/direct/schemata/logbroker)  
Проще и правильнее всего скопировать соседний файл, назвать новый файл как следует, а внутри поправить название топика и другие параметры, если требуется.  

Для продакшена/ТС/devtest — отдельные json, примеры:  
- Для прода — <https://a.yandex-team.ru/arc/trunk/arcadia/direct/schemata/logbroker/lbkx/direct/ess>  
- Для ТС — <https://a.yandex-team.ru/arc/trunk/arcadia/direct/schemata/logbroker/logbroker-prestable/direct/testing/ess>  
- Для devtest — <https://a.yandex-team.ru/arc/trunk/arcadia/direct/schemata/logbroker/logbroker-prestable/direct/devtest/ess>

## Ссылки

1. [Каталог с описаниями](https://a.yandex-team.ru/arc/trunk/arcadia/direct/schemata/logbroker)
1. [Инструкция для app-duty](../jeri/lb-create-objects.md)
