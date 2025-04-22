### Автор
[heliarian](https://staff.yandex-team.ru/heliarian)

## b-online-set-phrases-prices
Инлайновый конструктор ставок.
Используется на странице кампании для массового редактирования ставок условий показа.

## Внешний вид:
https://jing.yandex-team.ru/files/evolkowa/15-03-2018_16-56-39.png

## Состояния
Кнопка назначить бывает задизэйблена, когда от БК не приходят торги.
Протестировать этот кейс можно отключив их на своей бэте командой (выполнять из корня бэты):
`change-beta-settings --define BSRANK_URL=http://127.0.0.127/rank/24`
Включить обратно:
`change-beta-settings --reset`
