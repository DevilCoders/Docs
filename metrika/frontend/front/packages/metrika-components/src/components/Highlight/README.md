Подсвечивает текст по паттерну

```(jsx)
<Highlight pattern="екс сяко">
    Какой-то текст про всякое
</Highlight>
```

Можно использовать вложенные элементы
```(jsx)
<Highlight pattern="екс"><span>текст внутри span</span>, <span>а это текст внутри другого span</span></Highlight>
```

Можно задавать паттерны через пробел
```(jsx)
<Highlight pattern="екс утри"><span>текст внутри span</span>, <span>а это текст внутри другого span</span></Highlight>
```

И через массив
```(jsx)
<Highlight pattern={['екс', 'утри']}><span>текст внутри span</span>, <span>а это текст внутри другого span</span></Highlight>
```

Можно выделять бэкграундом
```(jsx)
<Highlight pattern="екс сяко" highlight="background">
    Какой-то текст про всякое
</Highlight>
```

Позиционный с подсветкой

```(jsx)
<Substr match={{ start: 2, end: 7 }}>This is my string</Substr>
```

Позиционный с подсветкой 2

```(jsx)
const search = require('utils/search');
const word = 'Metrika';
const sub = 'ika';
const match = search.createSearcher(sub)(word);

<Substr match={match} highlight="text">{word}</Substr>
```
