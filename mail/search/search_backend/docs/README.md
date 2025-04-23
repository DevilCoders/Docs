# Индексация
## Плохие практики
1) Если нужно обновить что то в индексе, никогда не делайте search then update, помните что у вас n реплик + между запросами может что то проиндексироваться (что то висит в очереди).
И конечно актуальны стандартные проблемы гонок, особенно если документы одного юзера могут обновляться параллельно
Используйте FieldFunctions, апдейты по условиям, док процессоры.  
## Апдейт всех документов по условию
```shell script
curl -D -  -X POST --data=@/tmp/update.json 'localhost:82/update?prefix=100500'
```

```json
{
  "prefix": "100500",
  "query": "id:my_document_100500_1005001",
  "docs": [
    {
      "field1" : "value1",
    }
  ]
}
```

**Всегда помнить про апдейты по непрефиксным условиям!**
 
## Апдейт при выполнении условия
Обновления документа не произодйет если под условие `query` попал хотя бы 1 документ
```json
{
  "prefix": "100500",
  "query": "id:my_document_100500_1005001",
  "UpdateIfNotMatches": true,
  "docs": [
    {
      "field1": "value1"
    }
  ]
}
```
## Простой апдейт
Объединения старых полей и полей из запроса в новый документ. Старый удаляется
```json
{
  "prefix": "100500",
  "docs": [
    {
      "id": "{my_document_type}_{prefix}_{doc_id}",
      "field1" : "value1",
      "field2" : "10"
    }
  ]
}
```
## Апдейт с докпроцессором
Если нужно во время индексации подтащить данные из другого документа
```json
{
  "prefix": "100500",
  "processor": {
    "pkjoin": {
      "query": "id:my_other_doc_100501",
      "get": "field3"
    }
  },
  "docs": [
    {
      "id": "{my_document_type}_{prefix}_{doc_id}",
      "field1" : "value1"
    }
  ]
}
```

## Апдейт с PreserveFields (aka modify-update)
Наличие поля `PreserveFields` превращает апдейт в модифай с особенностями. 
Ключевой кейс: мы хотим заменить документ в индексе (`/modify`) но хотим сохранить часть полей, например счетчики (показов/кликов/etc)

```json
{
  "prefix": "100500",
  "PreserveFields": ["field2"], // список полей которые сохранятся 
  "docs": [
    {
      "id": "{my_document_type}_{prefix}_{doc_id}",
      "field1" : "value1"
    }
  ]
}
```

Примеры выше могут комбинироваться друг с другом, за остальными примерами 
{% code '/mail/search/search_backend/test/java/ru/yandex/msearch/JsonIndexTest.java' lang='java' %}
## Общие примеры
Документ, id документа

```
[field.myfield]
prefix = true /false
stored = true / false
tokenizer = keyword/letter/lf
filter = lowercase
alias = xxx

```

stored / не stored поля - чем отличаются

field1 - префиксное, остальные нет

Превращение документа в ключи
```
id = doc100500
field1 = value1
field2 = value2
__prefix:

id = doc100501
field1 = value1
field2 = value3

10#value1 -> doc100500,doc100501
value2 -> doc100500
value3 -> doc100501

```

```
prefix: 567
        Письмо 1
hdr_subject: "Привет Зеркало" ->
        Письмо 2
hdr_subject: "Зеркало ты дурак" ->

567#Зеркало -> Письмо1 и Письмо2
567#Привет -> Письмо1
567#ты -> Письмо 2
567#дурак -> Письмо 2

prefix: 567
Письмо 1
hdr_subject: "Привет Зеркало" ->

prefix: 568
Письмо 2
hdr_subject: "Зеркало ты дурак" ->

567#Зеркало -> Письмо 1
567#Привет -> Письмо 1
568#Зеркало -> Письмо 2
568#ты -> Письмо 2
568#дурак -> Письмо 2

        Before update
          567#Зеркало -> Письмо 1
        After update
        567#Зеркало -> Письмо 1 (deleted) , Письмо 1
```

Письмо 1 -> список полей и значений - для получения &get=xxxx

/add
/modify
/delete
1) by id
2) by query

/update
1) simple
2) by query
3) if not matches
4) with preserve fields
5) with functions


