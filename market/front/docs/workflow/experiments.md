# Эксперименты

Большая часть задач в Маркете относится либо к написанию экспериментов, либо к выкладке удачных экспериментов.

Подробно об экспериментах написано в разделе [Регламент проведения AB-экспериментов на фронтенде Маркета v.2](https://wiki.yandex-team.ru/Market/Verstka/abt2).

Эксперименты с интерфейсами подразумевают быстрые и костыльные (второе требование не обязательно совсем) изменения в проекте, направленные на то, чтобы проверить какую-либо гипотезу.
Для каждого эксперимента создается свой флаг. Добавляются новые флаги посредством создания файла в каталоге `configs/flags_allowed.d`. В этих файла описываем эксперименты в формате:

```json
{
    "description": "{номер тикета}: {краткое описание эксперимента}",
    "manager": "{продуктолог}",
    "values": { // значения для экспериментов с несколькими сплитами
        "{название сплита}": "{описание сплита}"
    },
    "terminateTicket": "{тикет на удаление эксперимента}"
}
```

Весь код, написанный в рамках экспериментов оборачиваем в специальные комментарии, это позволит в будущем легко удалить неудачный или раскатить на 100% удачный эксперимент.
Комментарии выглядят примерно так:

```javascript
/**
 * @ifSuccess оставить doSomething() и переписать doSomethingElse()
 * @ifLose удалить все, кроме вызова doSomethingElse
 * @expFlag dsk_page-product_marketing-description
 * @ticket MARKETFRONT-34356
 * start
 */
    if (hasFlag(ctx.request, 'dsk_page-product_marketing-description')) {
        doSomething();
        doSomethingElse();
    }
/**
 * @expFlag dsk_page-product_marketing-description
 * @ticket MARKETFRONT-34356
 * end
  */
```

После написания эксперимента не надо жалеть времени на комментарии. С хорошими комментариями удалить или выкатить код можно будет в разы быстрей.
Идеально писать полную инструкцию по работе с кодом в случае выкладки или удаления эксперимента. Никогда не известно заранее кто будет выкладывать эксперимент, и если тебе может быть через пару недель понятен твой код, то коллега может потратить много времени на выяснение что чего и куда.
