#resize-watcher

##Описание
Отслеживает изменения высоты и/или ширины DOM-ноды или BEM-блока.
Родитель должен иметь в css position: 'relative'/'absolute'.

###Меинтейнеры
[cyn](https://staff.yandex-team.ru/cyn)

##Пример
```(js)
var watcher = BEM.blocks['resize-watcher'].getInstance({
    owner: $('body'),
    ignoreWidth: true,
    timeout: 50
});

watcher.on('change', function(e, data) {
    console.log('Изменилась высота `body`, теперь она составляет: ', data.height, 'px');
})
```
