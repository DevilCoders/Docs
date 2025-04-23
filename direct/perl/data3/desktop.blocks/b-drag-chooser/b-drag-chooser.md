r104847
Блок b-drag-chooser формирует список элементов которые можно выбирать (как один, так и несколько) и перетаскивать.
Так же возможно создавать группы элементов, где из нескольких вариантов выбрать можно только один.

### Использование

На примере b-statistic-columns-slices__item_type_slices.bemtree.xjst

```javascript
{
    block: 'b-drag-chooser',
    positions: this.data.group_by_positions, // расставляем пункты как нам необходимо
    value: this.data.group_by, // указываем какие из пунктов выбраны
    // передаем пункты, value будет проставлено чекбоксу, а text станет лейблом
    items: [
        {
            text: iget('Кампании'),
            value: 'campaign'
        },
        {
            text: iget('Метки'),
            value: 'tags'
        },
        {
            text: iget('Группы'),
            value: 'adgroup'
        },
        {
            text: iget('№ объявления'),
            value: 'banner'
        },
        {
            text: iget('Позиция'),
            value: 'position'
        },
        {
            text: iget('Место клика'),
            value: 'click_place'
        },
        {
            text: iget('Изображения'),
            value: 'has_image'
        },
        {
            text: iget('Тип устройства'),
            value: 'device_type'
        }
    ]
}
```
###Автор###
[belyanskii](https://staff.yandex-team.ru/belyanskii)
