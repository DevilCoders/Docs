#i-suggest-dataprovider#

##Описание##
Блок продоставляет данные для саджеста блока input.

##Меинтейнеры##
[ngraf](https://staff.yandex-team.ru/ngraf)

##Пример##
В bemhtml передает имя блока параметром в input
```javascript
{
    block: 'input',
    mods: { suggest: 'yes' },
    js: {
        dataprovider: { name: 'i-suggest-dataprovider' }
    }
}
```
в js добавляем доступные значения для подсказок
```javascript
this.findBlockInside('input')
    .getDataprovider().init(['a', 'b', 'c']);

```
