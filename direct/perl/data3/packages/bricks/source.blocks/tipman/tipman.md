# tipman

## Описание
Блок-обертка над блоком `tooltip`, помогает:
* Быстро использовать блок `tooltip`
* Задать проектные модификаторы для блока `tooltip` для подсказок, и в случае необходимости переопределить их
* Добавлять модификаторы на блока `popup` который используется внутри подсказки (оговорка: только те модификаторы, которые влияют на `js` попапа)
* Разруливает ситацию с необходимостью показать новый тултип при уже открытом (создает новый инстанс, старый закрывает с анимацией и удаляет)


### Меинтейнеры
[cyn](https://staff.yandex-team.ru/cyn)

## Пример
```
var tipman = BEM.create('tipman', {
    tipMods: { theme: 'normal' },
    tipMix: { block: 'tip-mix-block' },
    delay: 100,
    popupDirections: ['bottom', 'top'],
    onScrollClose: false
});

tipman.show({
    owner: errorDomElem,
    content: BEMHTML.apply({
        block: this.__self.getName(),
        elem: 'tooltip-message',
        content: errorText
    });
});
```
