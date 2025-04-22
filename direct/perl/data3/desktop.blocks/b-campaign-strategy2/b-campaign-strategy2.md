#Блок выбора и настройки стратегии рекламной кампании Директа

Отображает настройки текущей выбранной стратегии, при клике на Изменить открывает попап с b-strategy2-choose
Маппит старые стратегии в новые по принципам отсюда https://wiki.yandex-team.ru/users/coolisha/pererabotka-popapa-strategijj/#funkcionalnyetrebovanijaredaktirovat

##Мейнтейнеры
@a-urukov
@anyakey

##Модификаторы

– campaign-type – тип кампании Директа (по-умолчанию ТГО кампания). В нем передаются списки доступных стратегий и отключенных плафторм

##JS API

В блоке отсутствуют публичные методы и события. Вся работа осуществляется над data-model.

##Как добавить новую стратегию
1) В моду strategies добавить идентификатор стратегии (в основном шаблоне или в соответствующем модификаторе campaign-type)
2) В i-utils__strategy доопределить getTitleByName, getOptionsHint, getStrategyDescription и по необходимости getNameByPlatform, добавить новый ключ в STRATEGIES
3) Создать новый модификатор _name в b-strategy2-settings
4) Доопределить статический метод getModNameByStrategyName в b-strategy2-settings
5) Написать шаблон формы новой стратегии (не забывая об общих элементах b-strategy2-settings)
6) Задекларировать VM (наследуясь от b-strategy2-settings.vm.js)
7) По необходимости поправить маппинг

