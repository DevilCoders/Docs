# Сериалайзеры

Функционал сериалайзеров позволяет обрабатывать данные с сервера на стороне плеера. Он принимает данные "как есть" и трансформирует их в нужный плееру формат.

## Как пользоваться

### Описание

`PlayerUI.createHitApi(hitApi [, serializer='metrika'])`

* `hitApi` – объект с методами доступа к данным сервера (fetchHit, fetchHitsList, getVisitInfo)
* `serializer` – название сериалайзера или `false` для отключения сериализации ([доступные сериалайзеры](../lib/player/serializers)), по умолчанию `metrika`

### Пример использования

```javascript
// оригинальный hitApi
const model = {
  fetchHit(){
    // магия которая загружает данные с сервера
  },

  fetchHitsList(){
    // ...
  },

  getVisitInfo(){
    // ...
  }
}

// это то, что нужно передать плееру
const hitApi = PlayerUI.createHitApi(model, 'metrika')

PlayerUI.init({
  selector  : '.app',
  hitApi    : hitApi
}).then(player => {
  // тут подписываешься на события плеера, все как обычно
})
```

## Стандартный сериалайзер

Сериалайзер `metrika` рассчитывает, что данные ему приходят как есть, только `events` уже пропущен через `JSON.parse`

```json
{
  "profile": {
    //...
  },

  "result": {
    //...
    "events": [
      { ... },
      { ... },
      { ... }
    ]
    //...
  }
}
```

## Отключение сериализации

При необходимости сериалайзеры можно не использовать вовсе.

Это можно сделать двумя способами:

```javascript
PlayerUI.init({
  // ...
  hitApi: model
  // ...
})
```

или

```javascript
PlayerUI.init({
  // ...
  hitApi: PlayerUI.createHitApi(model, false)
  // ...
})
```

***Важно: методы `fetchHit`, `fetchHitsList` и `getVisitInfo` всегда должны возвращать Promise/A+ совместимый объект.

## Что под капотом

Сериалайзер представляет из себя объект с методами которые имеют имена аналогичные методам `hitApi`, т.е. метод сериалайзера `fetchHit` будет обрабатывать данные от этого метода из `hitApi`. Это значит, что если нам в дальнейшем понадобится процессить данные от других ручек – мы просто сможем расширить нужный сериалайзер без какого-то особого допиливания кода.

Метод `createHitApi` ищет совпадающие методы из `hitApi` и выбранного сериалайзера и патчит их встраиваясь в возвращаемые от методов `hitApi` промисы:

```javascript
// исходный метод hitApi
const model = {
  fetchHit(){
    return get('/hit/0')
  }
}

// метод сериалайзера
const serializer = {
  fetchHit(response){
    console.log(response)
    return response
  }
}

// итоговый метод (псевдокод)
fetchHit(...args){
  return model.fetchHit(...args).then(serializer.fetchHit.bind(model))
}
```

Если у сериалайзера отсутствует одноименный метод, то метод пропускается и пропатчен не будет.

Если метод `hitApi` возвращает что-то кроме промиса – будет выброшено исключение "HitApi::[название метода] should return Promise/A+ compatible object"

## Полезное

Пример инициализации: [server/static/pages/player.html](../server/static/pages/player.html)

Пример сериалайзера: [lib/player/serializers/metrika.js](../lib/player/serializers/metrika.js)

Исходник патчера: [lib/player/index.js](../lib/player/index.js?L=80#L80)
