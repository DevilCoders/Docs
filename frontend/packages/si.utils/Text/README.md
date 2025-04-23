# Text
Библиотека работы с текстом



##`uriEscape`

Кодирует строку.

#### Arguments
1. `str` *(String)*

##### Returns
*(String)*
#### Example
```js
uriEscape('Blah, (\'blah\'), blah!') => 'Blah, %28%27blah%27%28, %21'
```


* * *


##`xmlEscape`

Заменяет в заданной строке спецсимволы на соотв. entities.

#### Arguments
1. `str` *(String)*

##### Returns
*(String)*
#### Example
```js
xmlEscape('<&"\'`>') => '&lt;&amp;&quot;&#x27;&#x60;&gt;'
```


* * *


##`jsAttrEscape`

Экранирует символы '"/<>!- в строке;

#### Arguments
1. `str` *(String)*
2. `leaveEntities` *(Boolean)*: позволяет отключить экранирование для определенного27;


##### Returns
*(String)*
#### Example
```js
jsAttrEscape('&quot;&quot;') => '\\&quot;\\&quot;'
jsAttrEscape('""') => '\\u0022\\u0022'
```


* * *


##`decodeHtmlEntities`

Преобразует html entities в юникодные символы.

#### Arguments
1. `str` *(String)*


##### Returns
*(String)*
#### Example
```js
decodeHtmlEntities('&cent;') => '¢'
decodeHtmlEntities('&#162;') => '¢'
decodeHtmlEntities('&#x000A2;') => '¢'
```


* * *


##`trim`

Обрезает пробелы в начале и конце строки.

#### Arguments
1. `str` *(String)*

##### Returns
*(String)*
#### Example
```js
trim('  blah  ') => 'blah'
```


* * *


##`ltrim`

Обрезает пробелы в начале строки.

#### Arguments
1. `str` *(String)*

##### Returns
*(String)*
#### Example
```js
ltrim('  blah') => 'blah'
```


* * *


##`rtrim`

Обрезает пробелы в конце строки.

#### Arguments
1. `str` *(String)*

##### Returns
*(String)*
#### Example
```js
rtrim('blah  ') => 'blah'
```


* * *


##`firstUp`

Капитализирует первую букву строки.

#### Arguments
1. `str` *(String)*

##### Returns
*(String)*
#### Example
```js
firstUp('blah') => 'Blah'
```


* * *


##`supplant`

Заменят метки в строке на соответсвующие значение, переданные в объекте

#### Arguments
1. `str` *(String)*
2. `data` *(Object)*

##### Returns
*(String)*
#### Example
```js
supplant('Blah {first}, blah {second}', { first: 1, second: '2' }) => 'Blah 1, blah 2'
```


* * *


##`cut`

Обрезает строку до указанного размера;

#### Arguments
1. `str` *(String)*
2. `length` *(Number)*
3. `[hel='...']` *(String|Boolean)*

##### Returns
*(String)*
#### Example
```js
cut('Blah blah blah', 7) => 'Blah bl...'
cut('Blah blah blah', 7, true) => 'Blah bl\u2026'
cut('Blah blah blah', 7, 'CUSTOM_END') => 'Blah blCUSTOM_END'
```


* * *


##`smartCut`

Обрезает строку до указанного размера не разрывая слова;

#### Arguments
1. `str` *(String)*
2. `length` *(Number)*
3. `maxWord` *(Number)* если слово больше maxWord то его можно разорвать
3. `[hel='...']` *(String|Boolean)*

##### Returns
*(String)*
#### Example
```js
smartCut('Blah blah blah', 7) => 'Blah...'
smartCut('Blahblahblahblah', 7) => 'Blahbla...'
smartCut('Blah blah blah', 7, null, true) => 'Blah\u2026'
smartCut('Blah blah blah', 7, null, 'CUSTOM_END') => 'BlahCUSTOM_END'
smartCut('Blah blahblah blah', 7, 7) => 'Blah bl...'
smartCut('Blah blahblah blah', 7, 7, true) => 'Blah bl\u2026'
smartCut('Blah blahblah blah', 7, 7, 'CUSTOM_END') => 'Blah blCUSTOM_END'
```


* * *


##`reverse`

Реверс строки;
http://jsperf.com/string-reverse-test/2

#### Arguments
1. `str` *(String)*

##### Returns

#### Example
```js
reverse('pool') => 'loop'
```


* * *


##`reverseCut`

Обрезание строки с конца.

#### Arguments
1. `str` *(String)*
2. `length` *(Number)*
3. `[hel='...']` *(String)*: окончание обрезанной строки

##### Returns
*(String)*
#### Example
```js
reverseCut('Blah blah blah', 7) => '...ah blah';
reverseCut('Blah blah blah', 7, true) => '\u2026ah blah';
reverseCut('Blah blah blah', 7, 'CUSTOM_START') => 'CUSTOM_STARTah blah';
```


* * *


##`splitThousands`

Делит цифры в переданной строке на группы по 3;
в качестве дефолтного разделителя используется пробел.

#### Arguments
1. `num` *(Number|String)*
2. `[sep=' ']` *(String)*: разделитель
3. `byGost` *(Boolean)*: если значение true и число меньше 10000, возвращаем исходное число

##### Returns
*(String)*
#### Example
```js
splitThousands(100000) => '100 000'
splitThousands(100000, '+') => '100+000'
splitThousands(9999, ' ', true) => '9999'
```


* * *


##`fromPunycode`

Конвертирует строку из punycode представления.

#### Arguments
1. `str` *(String)*

##### Returns
*(String)*
#### Example
```js
fromPunycode('xn--d1acpjx3f.com') => 'яндекс.com'
```


* * *


##`smartWrap`

Делит заданную строку на колонки;

#### Arguments
1. `str` *(String)*
2. `[width=80]` *(Number)*
3.  *(String)*: разделитель
4. `softMode` *(Boolean)*: позволяет сохранять пробелы в конце слов

##### Returns
*(String)*
#### Example
```js
smartWrap('Load up on guns, bring your friends', 12, '<br>')
    => 'Load up on<br>guns,<br>bring your<br>friends'
```


* * *


##`convertRaw`

Заменяет в заданной строке маркеры на указанные теги.

#### Arguments
1. `str` *(String)*
2. `[length=str.length]` *(Number)*: длина, до которой следует обрезать входную строку
3. `[process]` *(Function)*: callback для обработки блока текста
4. `[otag='']` *(String)*: открывающий тег
5. `[ctag='']` *(String)*: закрывающий тег

##### Returns
*(String)*
#### Example
```js
convertRaw('Blah \u0007[TEST\u0007] \u0007[TEST\u0007] Blah', 0, '<b>', '</b>')
    => 'Blah <b>TEST</b> <b>TEST</b> Blah'

convertRaw('Blah \u0007[TEST\u0007] \u0007[TEST\u0007] Blah', 12, '<b>', '</b>')
    => 'Blah <b>TEST</b> <b>TEST</b>'

convertRaw('Blah \u0007[TEST\u0007] \u0007[TEST\u0007] Blah') => 'Blah TEST TEST Blah'

convertRaw('Blah \u0007[TEST\u0007] \u0007[TEST\u0007] Blah', 0, function(word) {
    return '<b>' + word + '</b>';
})
    => 'Blah <b>TEST</b> <b>TEST</b> Blah'
```


* * *


##`hash`

Вычисляет хеш из указанной строки.

#### Arguments
1. `str` *(String)*

##### Returns
*(String)*

#### Example
```js
hash('abc') => '375kp1'
```


* * *
