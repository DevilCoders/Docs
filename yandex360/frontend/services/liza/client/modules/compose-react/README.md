# Соглашения по разработке нового композа

## Глупые _ui-components_

Предлагается _ui-components_ воспринимать как "глупые" компоненты, которые ничего не знают о внешнем мире 
(о тех же сторах, например). 

В _ui-components_ мы не ссылаемся на _components_, так как у нас действует четкая градация:

* _components_ могут использовать и _ui-components_, и _components_;
* _ui-components_ могут использовать только другие _ui-components_. 

P.S. Изложил своё видение, сформированное благодаря советам от @chestnov. 
Предлагаю дополнять и уточнять этот README.


## Именование _CSS_-стилей

Придерживаемся следующих практик – блоки и элементы должны быть _PascalCase_, модификаторы – _camelCase_ 
(конвенция именования совпадает с https://en.bem.info/methodology/naming-convention/#react-style):

* `ComposeMyAwesomeComponent` – класс компонента _MyAwesomeComponent_
* `ComposeMyAwesomeComponent-Item` – элемент компонента
* `ComposeMyAwesomeComponent_withMod` – модификатор

Для удобства чтения группируем стили по тематическому признаку – 
[пример тут](https://wiki.yandex-team.ru/verstka/CSS/StyleGuide/#posledovatelnostsvojjstv).

Для удобного рефакторинга (и для будующего перехода на CSS Modules) рекомендуется выносить именна _CSS_-классов 
в отдельную переменную подобным образом:

```javascript
const blockClass = 'ComposeMyAwesomeComponent';

const classes = {
    Block: blockClass,
    Item: `${blockClass}-Item`,
    OtherItem_withMod: `${blockClass}-OtherItem_withMod`,
    Item_withStatus_danger: `${blockClass}-Item_withStatus_danger`
};
```

Тут есть отсупление от стилей именования _js_-переменных, но это промежуточное решение 
для удобства перехода на _CSS Modules_.


## Соглашения по _JavaScript_

Для удобочитаемости _JSX_ – выносим многострочные `classNames` в отдельную переменную подобным образом:

```javascript
render() {
    const classNames = cn(
        classes.Item,
        { [ classes.Item_active ]: isActive }
    );
    
    return (
        <ComposeMyAwesomeComponent className={ classNames }/>
    );
}
```
