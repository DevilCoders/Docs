
## Использование переменных
Переменные объекта
![alt text](https://wiki.yandex-team.ru/users/tulupov/.files/snimokjekrana2021-05-28v3.57.44pm.png)

**Пример вызова переменных:**
```sh
${obj.title}
${obj.order?.title?:'заказ не указан'}
```
Доступные переменные объекта можно посмотерть в описании объекта. 
Например, описание тикета можно посомтреть [тут](https://ow.tst.market.yandex-team.ru/metadata/ticket)

## Переменные в http 
### Парсинг  ответа 
[Варианты парсинга JSON ответов](https://github.com/json-path/JsonPath)  

Пример можно посмотерть [тут](https://github.com/json-path/JsonPath)

[Онлайн проверка выражения](https://jsonpath.com/)

**Текущий пользователь**
```sh
${beanFactory.getBean(ru.yandex.market.jmf.security.SecurityDataService).getCurrentEmployee()}
```
Но лучше использовать:
```sh
${api.security.employee}
```

