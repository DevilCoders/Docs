#b-feed-filter#

##Описание##
Блок фильтра по фиду

###Автор###
[heliarian](https://staff.yandex-team.ru/heliarian)

###Где используется###
Используется в блоках `b-group-feed-filter` и `b-feed-filters` в качестве основного содержимого

###Взаимодействие с другими блоками###
Пробуждает `live` блоки `b-group-feed-filter` и `b-feed-filters-group`

###Модели###
Список VM:

 - `vm-feed-filter` базовая модель для VM блока

Список DM:

 - `dm-dynamic-media-group` или `dm-dynamic-group` дата модель-контейнер (содержит в себе DM для VM)
 - `dm-feed-filter` дата модель

##Особенности##
Основан на блоке `b-dynamic-condition-row`

##Пример##

```
    {
        block: 'b-feed-filter',
        mods: {
            detailed: <detailed> ? 'yes' : ''
        },
        filter: <filter>
    }
```
