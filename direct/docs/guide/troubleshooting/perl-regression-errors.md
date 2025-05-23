# Ошибки в перловых регрессиях

## Ошибки B2B транспорта в БК

В паке тестов `BS Transport B2B` часто возникают ошибки вида
```
Проверка не пройдена: Данные транспорта на тестовом стенде отличаются от эталонного
Expected: the same objects of type LinkedHashMap
     but: the following fields are not the same:
CHANGED request XXX but expected YYY
```

В этом случае нужно сделать комментарий в тикете с регрессией, что упали такие-то тесты в паке `BS Transport B2B` и призвать
разработчика, чьи изменения это падение вызвали. Чтобы найти разработчика, можно посмотреть релизные тикеты и найти тот, в котором менялись поля `XXX` из лога.

Пример можно [посмотреть тут](https://st.yandex-team.ru/DIRECT-157319#61969906faa3541e1488cdaa).

Если разработчик говорит, что падение ожидаемо, надо убедиться в том, что падения связано только с разошедшимися полями, и ни с чем другим.

Корни проблемы растут вот откуда: на вики-странице про [B2B Транспорт в БК](https://wiki.yandex-team.ru/testirovanie/functesting/direkt/automatization/transport/b2b/) можно узнать,
что эти тесты запускаются на двух разных бетах (на одной `stable` пакет, на другой текущий `testing`), и сравниваются логи
двух запусков. Если в релиз попадают задачи, которые как-то изменяли формат полей или добавляли новые поля, то тесты начнут
ожидаемо падать, потому что `stable` пакет про эти изменения не знает. Для этого есть проперти `b2b.ignore.fields.list`.
Если перезапустить упавшие тесты с этой проперти и значением, указывающим на разошедшиеся поля, то, если других проблем нет, то тесты будут зеленые.
Так полезно делать, чтобы убедиться, что за этой ожидаемой ошибкой не спрятался какой-то неожидаемый баг.

Чтобы перезапустить автотесты в AQUA с этим полем, сначала нужно выписать все разошедшиеся поля. Смотрим, на какие поля ругается тест.
[В этом примере](https://aqua.yandex-team.ru/#/launch?id=6193a6808a903c5989fc5ace), если посмотреть логи, то можно увидеть, что тесты ругаются на поля
```
1/request/ORDER/*/CONTEXT/*/BANNER/*/Href
1/request/ORDER/*/CONTEXT/*/BANNER/*/HrefS2S
```
Для корректной установки поля `b2b.ignore.fields.list` исправляем наши поля следующим образом:
- перед `request` все удаляем и пишем `.+`
- заменяем все звездочки `*` на `.+`

В итоге получится:
```
.+request/ORDER/.+/CONTEXT/.+/BANNER/.+/HrefS2S
.+/request/ORDER/.+/CONTEXT/.+/BANNER/.+/Href
```
Соединяем все поля через запятую в одну строку
```
.+request/ORDER/.+/CONTEXT/.+/BANNER/.+/HrefS2S,.+/request/ORDER/.+/CONTEXT/.+/BANNER/.+/Href
```
Это и будет значением параметра `b2b.ignore.fields.list`.

Открываем [упавший пак из примера](https://aqua.yandex-team.ru/#/launch?id=6193a6808a903c5989fc5ace), и жмем на черную стрелочку:

![no alt](_assets/aqua-launch-black.png "черная стрелка")

В открывшемся окне скроллим содержимое до конца, и жмем на плюсик `+`:

![no alt](_assets/aqua-launch-black-plus.png "плюсик")

Появится новая строка с тремя полями:

![no alt](_assets/aqua-launch-black-empty.png "пустые поля")

В `Title` и `Key`пишем `b2b.ignore.fields.list`, в `Value` получившееся значение параметра `b2b.ignore.fields.list`:

![no alt](_assets/aqua-launch-black-filled.png "заполненные поля")

Жмем на кнопку `Restart Failed`.

Теперь, если все хорошо, тесты перезапустятся и будут зеленые.
