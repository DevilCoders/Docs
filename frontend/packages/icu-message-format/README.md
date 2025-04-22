# icu-message-format
Форматирование ICU Messages.

Для распарсивания сообщения в AST дерево
используется пакет `messageformat-parser`

Цель превратить такое сообщение:
```
{eventType, select, concert {{tagCase, select, many {Концерты {inCity}} other {Концерт {inCity}}}} theatre {{tagCase, select, many {{dateType, select, none {Спектакли {inCity}} month {Спектакли {inCity}, {datePreview}} months {Спектакли {inCity}: {datePreview}} other {Спектакли {inCity} {datePreview}}}} other {{dateType, select, none {Спектакль {inCity}} date {Спектакль {inCity}: {datePreview}} other {Спектакль {inCity} {datePreview}}}}}} other {Расписание {inCity}}}
```

В читаемое, для редактирования в танкере вручную:
```
{eventType, select,
    concert {{tagCase, select,
        many {Концерты {inCity}}
        other {Концерт {inCity}}
    }}
    theatre {{tagCase, select,
        many {{dateType, select,
            none {Спектакли {inCity}}
            month {Спектакли {inCity}, {datePreview}}
            months {Спектакли {inCity}: {datePreview}}
            other {Спектакли {inCity} {datePreview}}
        }}
        other {{dateType, select,
            none {Спектакль {inCity}}
            date {Спектакль {inCity}: {datePreview}}
            other {Спектакль {inCity} {datePreview}}
        }}
    }}
    other {Расписание {inCity}}
}
```

Пример вызова:
```ts
import { format } from '@yandex-int/icu-message-format'

const msg = 'Such { thing }. { count, selectordinal, one {First} two {Second} few {Third} other {#th} } word.'

const formattedMsg = format(msg);
```
