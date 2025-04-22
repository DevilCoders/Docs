#Calendar

Портирован из [web4](https://github.yandex-team.ru/serp/web4/tree/dev/contribs/calendar).

![calendar](https://github.yandex-team.ru/search-interfaces/o2-calendar/raw/master/preview/desktop.png)
<br/>
На iOS и Android используется системный календарь.

## Пример использования

```js
<Calendar
    readonly={true}
    weekdays={['пн', 'вт', 'ср', 'чт', 'пт', 'сб', 'вс']},
    months={['Январь', 'Февраль', 'Март',
        'Апрель', 'Май', 'Июнь',
        'Июль', 'Август', 'Сентябрь',
        'Октябрь', 'Ноябрь', 'Декабрь']},
    val={'11.11.2015'}
/>
```
Есть возможность установить ограничения на выбор даты с помощью полей `earlierLimit` и `laterLimit`.
```js
<Calendar
    readonly={true}
    weekdays={['пн', 'вт', 'ср', 'чт', 'пт', 'сб', 'вс']},
    months={['Январь', 'Февраль', 'Март',
        'Апрель', 'Май', 'Июнь',
        'Июль', 'Август', 'Сентябрь',
        'Октябрь', 'Ноябрь', 'Декабрь']},
    earlierLimit={'11.10.2015'},
    laterLimit={'11.12.2015'},
    val={'11.11.2015'}
/>
```
![calendar](https://github.yandex-team.ru/search-interfaces/o2-calendar/raw/master/preview/limits.png)
