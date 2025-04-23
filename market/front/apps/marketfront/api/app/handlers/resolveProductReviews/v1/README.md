# Резолвер resolveProductReviews

## Описание

Резолвер, способный вернуть отзывы на продукт вместе с пользователями, которые их оставили.
Умеет сортировать и фильтровать выдачу отзывов. Единственный обязательный параметр - `productId`.

_Сущность user была переименована в publicUser._

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/review/helperTypes.js#L11-L38)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/modelOpinion/modelOpinion.json)
- [Описание сущности `отзыв` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/review/index.js)

**WARNING**: микроформат устаревший и может не соответствовать действительности.

FAQ:

> На фронте есть значок "проверенный покупатель". Где он тут?

Это поле `isCpa`. Говорит о том, что пользователь покупал когда-то этот товар на маркете через CPA.

> На фронте есть время использования. А в данных где?

Это числовое поле `usage`. Мы его интерпретируем вот [так](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/app/node_modules/dictionary.js#L110-L118).

> Почему фильтр по оценкам принимает -2 от 2, а не от 0 до 5? И возвращает такие же значения.

Так сложилось исторически. Когда-то на Маркете оценки выставляли и отображали именно так.
Поэтому к оценкам нужно делать +3, если нужна шкала [1, 5];
