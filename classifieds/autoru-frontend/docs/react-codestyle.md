# React codestyle

[Как именовать все в React'е](./react-naming.md)

Для истории – комитет™ давным-давно решил [так](https://wiki.yandex-team.ru/vertis/frontend/react/).

Пока плоским списком...

1. **`.js` vs `.jsx`**. Везде используем `.js`, потому что использование другого расширения будет сложно контроллировать и будут ненужные переименования `.js <-> .jsx`. 

1. **`import` vs `require` и свалки типа util.js**.
Выбираем `require`, чтобы не путаться, т.к. файлы могут использоваться как в ноде, так и в реакте. Если кто-то найдет простой способ гарантирования, чтобы в файлах исполняемых в node.js отсутствовали import/export, правило можно будет поменять.
Из-за `require` мы теряем tree-shaking в webpack, соответственно весь код из свалки `util.js` попадет в бандл, раздует его размер, и приедет в браузер. Компенсируем это тем, что не делаем свалок из функций. Надо разделять хелперы на отдельные файлы, покрывать их тестами и рекварить по необходиости.

1. **Структура action**. Все `type` должны быть константами, строки использовать нельзя.
```
{
    "type": "СТРОКОВАЯ_КОНСТАНТА",
    "payload": "данные экшена"
}
```

5. **Именование action**. Все константы лежат в файле `actionTypes.js` (http://redux.js.org/docs/basics/Actions.html).
```
"MY_ACTION" - синхронный
"MY_ACTION_PENDING" - асинхронный, начало
"MY_ACTION_RESOLVED" - асинхронный, завершился удачно
"MY_ACTION_REJECTED" - асинхронный, завершился неудачно

"STORENAME_FETCH" - хорошее название
"FETCH_STORENAME" - плохое название, плохо визуально группируются. 
```

6. **Коллбэки или строки в ref**
В официальной документации React написано, что использование строк является устаревшим способом получения ссылки на DOM элмент.
В будущих версиях React эта возможность скорее всего будет удалена. Предпочтительным способом является коллбэк в атрибуте ref.
https://facebook.github.io/react/docs/refs-and-the-dom.html#legacy-api-string-refs
Пример.
```
// wrong
<div ref="domNode" />

// correct
<div ref={ node => this.domNode = node } />
```

## Где хранить actions, reducer, selectors

В проекте есть папка `dataDomain`, для каждого куска данных там создается отдельная папка, где лежат reducer, action'ы и selector'ы. Внутри папки лежат следующие файлы:
* `actionTypes.js` - ENUM со списком доступных экшенов
* `reducer.ts` - redux reducer
* `actions/` - папка с экшенами. Каждый экшен лежит в отдельном файле
* `selectors/` - папка с селекторами. Селектор - чистая функция от `state`, которая возвращает какие-то данные из соответствующего стора. Она избавляет от копирования однотипных селекторов по mapStateToProps. При необходимости можно оборачивать в `reselect`. Каждый селектор лежит в отдельном файле.

Пример:
```
<project-dir>/
    react/
        dataDomain/
            favorites/ /* кусок данных "избранные объявления"
                actionTypes.js
                reducer.ts
                actions/
                    add.js 
                    fetch.js
                    remove.js
                selectors/
                    getList.js
                    includesOffer.js 
                    
```

Пример использования селекторов:
```
const isOfferInFavoriteList = require('data-domain/favorites/selectors/includesOffer');

class FavoriteButton extends React.Component {
    // ...
}

const mapStateToProps = (state, ownProps) => {
    return {
        checked: isOfferInFavoriteList(state, ownProps.offerId),
    };
};

module.exports = connect(mapStateToProps)(FavoriteButton)
```

```
const getFavoritesList = require('data-domain/favorites/selectors/getList');

class FavoritesListPopup extends React.Component {
    // ...
}

const mapStateToProps = (state) => {
    return {
        list: getFavoritesList(state),
    };
};

module.exports = connect(mapStateToProps)(FavoritesListPopup)
```
