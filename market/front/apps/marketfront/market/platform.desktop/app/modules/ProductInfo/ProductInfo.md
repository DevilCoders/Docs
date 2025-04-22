#Модуль ProductInfo

## Что умеет
По айдишнику получить базовую информацию о модельке (и гурушной, и кластере)
и вернуть их в едином формате.

## Как

```js
var productId = this.request.params.productId;

this
    .push(this.module(require('app/modules/ProductInfo'), {
        id: Number(productId),
        user: this.user,
        request: this.request
    }), 'ProductInfo')
    .push(setProduct);


    function setProduct(productData) {
        var product = productData.getInfo();
    }
```

## Почему
Так исторически сложилось(с), что инфа о моделях, созданных вручную лежит в гуре, а о сгенеренных автоматически
в репорте. Пространство айдишников у них теперь общее, а вот ручки в бекенде, которая бы сама понимала,
что это за моделька нет. Поэтому приходится дергать сначала гуру, если в ее ответе ничего не находится,
то дергать репорт.
