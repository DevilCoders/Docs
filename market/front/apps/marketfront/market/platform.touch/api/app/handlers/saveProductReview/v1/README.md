# Резолвер saveProductReview

## Описание

Резолвер, который создает и обновляет оценку/отзыв на товар. Необходима авторизация.
Возращает созданный отзыв.

Оценка - это кол-во звёз которое выставил пользователь и не указал никаких других полей
Отзыв - это оценка с текстовым описание от пользователя

Самая главная особенность: сохранение отзыва для пары продукт+пользователь каждый новый раз создаёт новую версию отзыва.
Поэтому опираться на идентификатор отзыва не имеет смысла.

Обязательные параметры:
- _productId_ - айдишник товара;
- _averageGrade_ - оценка от 1 до 5;

Важный, но не обязательный параметр:
 - _source_ - источник(страница с который мы пришли на форму оставления отзыва). Если не указан, проставляется `main`

Детальнее в [тикете](https://st.yandex-team.ru/MARKETVERSTKA-25980#5a6f264a1878cd001b842e6b)

Инфа по сорсам собирается и отображается на [графике](https://grafana.yandex-team.ru/d/000018139/pers-tms-grade-stats-temp?orgId=1&from=now-7d&to=now)

Необязательные параметры:
- _type_ - 1 - модель, 2 - кластер
- _pro_ - текст с достоинствами
- _contra_ - текст с недостатками
- _comment_ - текст комментария
- _anonymous_ - 0 - обычный пользователь, 1 - аноним, 2 - черновик
- _usage_ - 0 - 'Меньше месяца', 1 - 'Несколько месяцев', 2- 'Больше года'
- _factors_ - массив с факторами в формате `{id: ... , value: ...}`
- _photos_ - массив с фотками в формате `{groupId: ..., imageName: ...}`
- _recommend_ - `true|false` рекомендация товара

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/saveProductReview/v1/index.js#L24)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/modelOpinion/modelOpinion.json)
- [Описание сущности `отзыв` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/review/index.js)
