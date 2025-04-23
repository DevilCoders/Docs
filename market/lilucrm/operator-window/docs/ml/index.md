# Quick start
### Первый скрипт
1) Зайти на тестовый [стенд EO]((https://ow.tst.market.yandex-team.ru/admin))
2) В область с названием **Скрипт** вставить код ниже:
```groovy
def ticket =  api.db.get('ticket@128474894')
return ticket.taximlSupport
```
Получи id  категории, которую нам возвращает такси.


