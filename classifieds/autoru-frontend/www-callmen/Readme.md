# HTTP-Сервис преобразования параметров в ЧПУ

## как зовут
`af-callmen`

## где живет
`af-callmen-web.vrts-slb.test.vertis.yandex.net` – в тесте

`af-callmen-web.vrts-slb.prod.vertis.yandex.net` – в бою


## Особенности

### Хост

dev живёт на `dev.vertis.yandex-team.ru`

### Открывается по GUID заявки

```
https://callmen.frontend.<LOGIN>.dev.vertis.yandex-team.ru/edit/<GUID>/
```

Которую можно сделать в [тесте](https://test.avto.ru/my/credits/wizard/)

Достаточно заполнить **личные** или **паспортные** данные

## Идеи

Для того чтоб было "проще", лучше присылать с клиента не новое состояние, чтоб не считать diff всё время, а команды на изменение и тогда считать новое состояние "машины" и возвращать то что нужно отобразить на клиенте.

### Про Рефакторинг

Продолжаем кастылить и таких моментов будет больше чем кажется, имхо надо рефакторить в сторону [стейт машины](https://github.com/davidkpiano/xstate), пока не поздно. Чтоб у нас всё это как-то описывалось в одном месте +/- Тогда всю эту @уйню можно будет даже визуализировать!

Где боли (чуть подробнее чем везде)
  * [prepareCreditApplicationForSecureUsing](./react/preparers/prepareCreditApplicationForSecureUsing.js)
  * [updateCreditApplicationShark](./app/api/blocks/updateCreditApplicationShark.js)
  * упраление visible

### Про состояния (черновик)

Стостояния контролов зависит от того кто смотрит
  * заполнен и скрыт (не владелец)
  * не заполнен (не важно)
  * заполнен не скрыт (владелец)

Состояние блоков - есть логика заполнения или нет
можно включать на condition - изменение

Есть ещё какая-то логика на то что отображаем, в зависимотси от ...

Если меняет не владелец, то гидрируем, потом применяем тоже что в [mapCreditFormValuesToCreditApplication](../auto-core/react/dataDomain/credit/mappers/mapCreditFormValuesToCreditApplication.ts)

Если заполнен и скрыт, и есть логика заполнения как с `is_the_same_address`, нужно где-то держать `borrower` - как гидрировать и какую логику применять или и дальше писать [такую дичь](./app/api/blocks/updateCreditApplicationShark.js)
