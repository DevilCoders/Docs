# Vacuum - сервис обработки кластеров диалогов для нужд модерации

В Вертикалях существует сервис [Dust](../../etc/dust/design.md), который умеет кластеризовать диалоги, в которых участвуют наши пользователи.
Источником диалогов являются чаты и расшифровки звонков по нашим подменным номерам телефонов.

Сервис Vacuum существует для того, чтобы потреблять результаты работы [Dust](../../etc/dust/design.md) и
использовать их для нужд группы качества контента. Силами модераторов мы можем размечать кластера диалогов как мошеннические
или спамерские и на основе этого банить соответствующих пользователей на сервисах. 

Также мы можем накапливать информацию об анонимных пользователях, так как в телефонных разговорах участвуют пользователи,
которые необязательно зарегистрированы на наших сервисах. Это позволит банить таких пользователей при регистрации.

##### Для обеспечения такого функционала, сервис `Vacuum` должен решать следующие задачи: 
- Отправка интересующих нас кластеров диалогов на разметку в [hobo](../hobo/README.md)
- Хранение результатов разметки кластеров
- Оповещение сторонних сервисов (в первом приближении [модерации](to-do)) об изменении принадлежности пользователя к размеченным кластерам
- Предоставление API для получения разметки по определенному пользователю

В качестве основного фокуса при проектировании сервиса предлагаю принять максимальное уменьшение связности между `Vacuum`
и сервисом модерации. Поэтому за пределами ответственности сервиса предлагаю оставить следующие процессы:
- Принятие решения о бане пользователя на основе разметки его диалогов
- Оповещение продуктовых сервисов или [телепони](../../etc/telepony/README.md) о бане пользователя/телефона/диалога

## Основные понятия
С описанием сущностей, предоставляемых [Dust](../../etc/dust/design.md) можно ознакомиться в их документации.
В данном документе введем дополнительные ограничения:
- `кластером` диалогов будем называть то, что в [Dust](../../etc/dust/design.md) называется `мастер-кластером` - т.е. кластером с консистентным id
- под `идентификатором пользователя` будем понимать уникальный идентификатор участника диалога (телефон/паспорт id/autoru user id).
- `разметкой кластера` будем называть вердикт от модераторов о принадлежности кластера к тому или иному типу диалогов (мошеннический/спамерский/...) - [модель](./markup.md)

## Входные данные

### Dust
[Dust](../../etc/dust/design.md) предоставляет нам 2 интерфейса в качестве источника входных данных:
топик в кафке с [событиями о результатах кластеризации](../../schema-registry/proto/dust/clustering_results_model.proto) 
и [gRpc api](../../schema-registry/proto/dust/dialogs_api.proto) для работы с диалогами и кластерами.

`События кластеризации` обязательно содержат поля:
- id кластера
- версия кластера  
- id диалога

### Hobo/Api
`Vacuum` потребляет события об изменении разметки кластеров от `Hobo`.
Такие же события могут быть переданы в синхронное апи для ручного изменения разметки по известным кластерам.

## Компоненты
![](./img/components.svg)

### API
ToDo

### Обработчик событий Dust
ToDo

### Обработчик событий Hobo
ToDo

### Хранилище
ToDo. 
О чем нельзя забыть:
- Первичным ключом кластера должен быть не только id кластера, но и его версия. 
  В процессе эволюции ml кластера могут меняться - разбиваться на 2 кластера/объединяться и тд.
- Нужно решить храним ли мы у себя диалоги или нет

## Основные сценарии работы

Инициаторами любых процессов связанных с обработкой кластеров могут выступать либо [Dust](../../etc/dust/design.md) либо 
модераторы (через апи или закрытие задачи в хобо).

### Обработка события от Dust

Процесс обработки [события]((../../schema-registry/proto/dust/clustering_results_model.proto)) о кластеризации очередного 
диалога от [Dust](../../etc/dust/design.md) зависит от 3х параметров:
1. известен ли нам кластер, в который попал очередной диалог
2. совпадает ли версия присланного кластера с той, что сохранена у нас
3. размечен ли у нас уже кластер, в который попал диалог

В зависимости от этих 3х параметров выбираем следующие сценарии:
![](./img/dust_processing.svg)

1. Получили информацию о диалоге и мы ничего не знаем о кластере, в который этот диалог попал:
    - Заводим кластер с пустой разметкой

2. Получили информацию о кластере, версия которого изменилась, но старая еще не была размечена:
    - сохраняем новую версию кластера
    - удаляем старую

3. Получили информацию о кластере, версия которого изменилась, и старая версия уже была размечена:
     - Самый не проработанный сценарий. Пока не знаем что делать, потому что не знаем в каком виде нам это будут доставлять

4. Получили информацию об актуальном, но не размеченном кластере
      - Копим информацию о кластере, необходимую для принятия решения об отправке его на разметку (пока что думали про кол-во диалогов)
      - На основе этой информации принимаем решение об отправке кластера на разметку в Hobo (например если кол-во диалогов превысило порог)
    
5. Получили информацию о диалоге и кластер, в который попал этот диалог активен и уже размечен:
    - проверяем чем размечен кластер
    - отправляем в модерацию непустую разметку
    
### Обработка события от Hobo/запросов в апи
В целом события от хобо/апи не должны сильно различаться, поэтому пока что объединяю их в один пункт.
Пока не понятно содержимое этих самых событий, поэтому описывать сценарии сложно. 
Все таки постараюсь описать основные моменты, которые, как кажется, должны присутствовать в любом решении

Событие от хобо/запрос в апи должны содержать информацию об изменении разметки того или иного кластера.

После получения такого события мы должны проитерироваться по всем диалогам, входящим в этот кластер (диалоги наверняка
можно не хранить, а получить из dust) и уведомить модерацию об изменении разметки этих диалогов.

При этом итерация по кластеру может занимать неопределенное время во время которого могут происходить разные события:
- итерация прервется(из-за перевыкладки или чего угодно еще) - нужно подумать о том, нужно ли хранить стейт или просто начинать заново
- получение любого события об этом же кластере(мы в процессе снятия банов с кластера, а модератор решил снова пометить его как "плохой") - подумать что делать

### Оценка объемов

ToDo. Предположительно < 1000 кластеров первоначально. Объем диалогов уточнить у Никиты.

### ToDo
- Никак не описана работа с метой кластеров. Храним ли мы ее или заставляем хобо ходить за ней в Dust.
- Если отправкой банов в телепони будет заниматься модерация, то как мы будем банить пользователей, которых нет в модерилке?

