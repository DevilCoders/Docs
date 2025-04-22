# Работа с жизненным циклом объекта

API для работы с жизненным циклом объекта позволяет получить информацию о возможных статусах бизнес-объекта, а так же 
возможности перехода в другой статус.

У бизнес-объектов с жизненным циклом есть атрибут status, который содержит код статуса жизненного цикла.

```groovy
def obj = ...
def code = obj.status
```  


1. `api.wf.getStatus(obj)` возвращает полную информацию о текущем статусе объекта.
  Пример:
  ```groovy
def obj = ...
def status = api.wf.getStatus(obj)
def code = status.code // код статуса 
def title = status.title // название статуса
def archived = status.archived // признак архивности бизнес-объектов. Объекты находящимися в статусе, где true == status.archived, считаются архивированными.
if (status.hasTransition('otherStatusCode')) { // проверяет возможность перехода в статус с указанным кодом
  ...
}
```
2. `api.wf.hasTransitionTo(obj, status)` проверяет наличие перехода из текущего статуса бизнес-объекта в указанный статус. 
По своей сути является короткой запьсю для `api.wf.getStatus(obj).hasTransition(status)`.
  Пример:
  ```groovy
def obj = ...
if (api.wf.hasTransitionTo(obj, 'otherStatusCode')) {
  ...
}
```   