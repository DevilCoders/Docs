## Приложение "Везёт" для водителей

### Описание

Делаем второе приложение для водителей. Продуктовое описание [тут](https://wiki.yandex-team.ru/taxi/partnerproducts/Buber/#otkrytyevoprosy)


### Продуктовые ограничения

Бекенд должен позволить мультиапить одному водителю в двух приложениях. 
Соответственно, для водителя должны открываться две независимые сессии в двух приложениях, у них должно быть два статуса,
два независимых GPS-трека, независимый диспатч заказов и раздельные показатели (рейтинг, лояльность, активность и т. д.).

При этом таксопарку без разницы, в каких приложениях его сотрудники выполняют заказы, в идеальном варианте для парка 
профиль водителя должен выглядить единым.

Поддерживаем эти требования компромиссным вариантом - делаем для парков отдельную диспетчерскую с профилями водителей 
в Везёт. Пользователи, настройки прав доступа, условия работы, водители и машины поддерживаются в синхронизированном 
состоянии: все основные данные из основной диспетчерской переливаются в диспетчерскую Везёт.

````markdown
<details>
  <summary>Почему делаем именно так</summary>
Рассматривали несколько вариантов, как поддержать два профиля в диспатче, но один - в парке:
1. Оставить один профиль водителя, но раздвоить его в трекере и показателях - максимально удобно для парка, но требует 
масштабных изменений в расчете показателей по водителю и умеренные изменения в диспатче
2. Сделать два дублирующих профиля водителя в парке: полностью ломает диспетчерскую как продукт, но зато не требует 
доработок в других частях Такси
3. Сделать для парков отдельную диспетчерскую с профилями водителей в Везёт: делает работу таксопарка несколько 
неудобнее, не требует доработок в других частях такси.
Выбрали третий вариант.

Также был вопрос, что делать с unique-driver. Можно оставить unique-driver общим для Везёт и Таксометра, можно разделить.
Какое было бы поведение системы в обоих из этих вариантов написано тут:
https://wiki.yandex-team.ru/taxi/partnerproducts/Buber/#zapisivdbtaxi.uniquedrivers
Решили оставить общий и перевести наиболее критичные метрики на идентификатор - пару (unique-driver, app-family)</details>
````  

## Архитектура

### Влияние на цикл заказа

Потребуется отключить активность для водителей и заказов Везёт.

### Компоненты

#### Клиент

Клиент отдельный, переиспользует часть кода Таксометра, часть редизайнит, часть переделывает полностью.
Ходит на бекенд в те же API, что и Таксометр, но использует отдельный юзер-агент:
```
Taximeter-Vezet <version>
```

####БД dbparks.parks

В dbparks.parks добавляется поле:
```
{
    "_id": "70625da32a4e42598b569d80227a80ce",
    ...
    "fleet_type": undefined|"vezet",  # тип приложения, с которым работает диспетчерская
}
```

####Сервис синхронизации парков taxi-fleet-synchronizer
Сервис выполняет синхронизацию основной и Везёт-диспетчерских путём копирования данных в коллекциях 
dbparks.parks, dbcars.cars, dbdrivers.drivers, work-rules, пользователей и групп пользователей.

Для хранения маппингов используется PostgreSQL с набором табличек унифицированной структуры для всех копируемых сущностей.

Копирование производится набором регулярных задач. Задачи синхронизации должна быть возможность запускать в виде скрипта.

API сервиса:
- по id сущности отдать список связей. если сущность корневая, отдаёт наследников, если наследник - отдаёт корневую (будет использоваться во взаимозачёте фотоконтроля)
- создать синхронизированного водителя в парке-наследнике (будет использоваться при первом логине, 1-5 rps)


### Этапы (партнёрские продукты)
I. То, что обязательно сделать до технического запуска:
1. Заводим микросервис, отвечающий за синхронизацию диспетчерских - taxi-fleet-parks-mirror
2. Джоба/скрипт заведения дочерних диспетчерских Везёт - py3 или uservices
Заводим конфиг-3.0 по городам, включающий Везёт паркам.
Делаем джобу, инкрементально синхронизирующую все изменения из всех основных диспетчерских в Везёт. Для диспетчерских 
в городах с включенным конфигом также создаём новую диспетчерскую, если её ещё нет.
Делаем возможность запустить джобу как скрипт, чтобы при включении города можно было создать дочерние диспетчерские 
во всех существующих парках.
Скорее всего будет достаточно копировать документы в dbparks.parks (нужно проверить). API здесь использовать пока не 
получится, т. к. существующие API дробят диспетчерскую на несколько сущностей и пока что покрывают не все поля из базы.
Если копирования документа будет недостаточно, можно свериться с логикой из C# DomainService.CreateNewPark
В целях тестирования можно завести одну мастер-учётку в парке апишкой https://github.yandex-team.ru/taxi/uservices/blob/develop/services/dispatcher-access-control/docs/yaml/api/v1_users.yaml#L12
3. Заведение профиля водителя в диспетчерской Везёт на логине. - backend-cpp
Когда предлагаем список парков в логине Везет, ищем телефон водителя в таксометровых парках и предлагаем на выбор их потомков.
Пишем ручку, копирующую водителя, машину и условие работы из основной диспетчерской в дочернюю по запросу.
При логине в Везёт дергаем ручку копирования.
На клиент в логине отдаем время, которое необходимо подождать, чтобы новый водительский профиль пророс в кеши - грязное, но дешёвое решение.

II. То, что нужно сделать для продуктового запуска:
3. Делаем честный инкрементальный кеш водителей и машин в driver-protocol - backend-cpp
Сейчас кеш полностью обновляется раз в 5 минут. При этом полное обновление кеша производится дольше, чем 5 минут,
поэтому водители доходят до кеша в среднем за 5 минут.
Делаем как в parks: инкрементальный апдейт идет постоянно. Полный запускается в фоне, раз в 1-2 часа.
Note: Синкнуться с Володей Скругиным. Вероятно, уже есть переиспользуемое решение.
4. Джоба синхронизации условий работы - py3 или uservices
С некоторой периодичностью вычитываем все парки с fleet_type:vezet, копируем все условия работы из родительского парка
в дочерний.
5. Джоба синхронизации машин и водителей - py3 или uservices
Синхронизируем только существующие. Абсолютно все не копируем, иначе могут взорваться кеши в driver-protocol.
Инкрементально вычитываем все машины, апидейтим дочерние, сверяясь с маппингами
Затем инкрементально вычитываем водителей, апдейтим по parent_driver_id
6. Джоба синхронизации пользователей и групп - py3 или uservices или C#
С некоторой периодичностью по всем паркам с fleet_type:vezet синхронизируем группы и пользователей, как с условиями работы.
Откладываем эту задачу в конец.
Если успеваем сделать все ручки из тикета https://st.yandex-team.ru/TAXIMETERBACK-7266, то делаем джобой на py3/c++.
Если не успеваем - временно хардкодим перекладывание ключей в редисе в C#.
При синхронизации все роли делаем как read-only, чтобы в дочерней диспетчерской нельзя было ничего менять
7. Взаимозачёт фотоконтроля - py3
Требуется делать взаимозачем при прохождение фотоконтроля. При создании нового водителя Везет - копировать ему состояние экзаменов.
Расширяем взаимозачёт фотографий и резолюций в C# - 3d.

