# Правила Char

Правила типа `char` обрабатываются специальным Remorph-модулем и позволяют описывать обычные посимвольные регулярные выражения. В режиме матчинга такие регулярные выражения будут срабатывать не на отдельных токенах исходного текста, а сразу на предложениях целиком.

В этом основное отличие регулярных выражений Char-модуля от посимвольных регулярных выражений [обычного Remorph-модуля](rules-remorph.md), с помощью которых задаются условия на отдельные слова. Важно заметить, что матчинг происходит с учетом границ токенов: итоговый матч не может начинаться или заканчиваться в середине слова, он может захватить только группу слов.


## Правила {#pravila}

Правила описываются `rule`-предложениями с использованием специального синтаксиса для описания регулярного выражения:

```
rule <name> = /<регулярное выражение>/<модификаторы>;
```

Правилу можно задать приоритет, задаваемый вещественным числом, и по умолчанию равный единице.

```
rule <name> (<priority>) = /<регулярное выражение>/<модификаторы>;
```


## Определения {#opredelenija}

Кроме правил можно описывать определения - макросы, которые могут быть подставлены в регулярные выражения в виде ссылок. Для этого используются `def`-предложения.

```
def <name> = /<регулярное выражение>/<модификаторы>;
```


## Регулярные выражения {#reguljarnyevyrazhenija}

В Char-модуле используются посимвольные регулярные выражения, задаваемые с помощью специального синтаксиса:

```
/тело регулярного выражения/модификаторы
```

Регулярные выражения работают над Юникодом. Когда речь идет о символах - речь идет о юникодных символах, а не об отдельных байтах.

Для описания символов или классов символов в регулярных выражениях используются следующие конструкции:

- `.` любой символ (класс "все символы");
    
- `\x` escape-последовательность (см. [ниже](#jekranirovanieiescape-posledovatelnosti));
    
- `[...]` класс символов (см. [ниже](#klassysimvolov));
    
- `@{name}` подстановка определения с именем `name`;
    
- любой другой символ, кроме операторов, представляет себя самого.

Для представления операторных символов нужно использовать экранирование.

В выражениях используются следующие операторы:

- `(...)` группировка;
    
- `(<name>...)` группировка с захватом заматченных символов в именованную группу `name`;
    
- `X|Y` альтернатива между X и Y;
    
- `X{n}` повторение X n раз;
    
- `X{n,m}` повторение X от n до m раз;
    
- `X{n,}` повторение X любое количество раз, но не меньшее, чем n;
    
- `X?` опциональный символ X (аналогично `X{0,1}`);
    
- `X*` повторение символа X любое количество раз, в том числе его отсутствие (аналогично `X{0,}`);
    
- `X+` повторение символа X любое количество раз, но не менее одного раза (аналогично `X{1,}`);
    
- `^` начало текста;
    
- `$` конец текста.
    

Модификаторы определяют специальные режимы работы регулярного выражения. На данный момент доступен только модификатор `i`, делающий выражение регистронезависимым.

Пример: `/[a-zA-Z]/` и `/[a-z]/i` идентичны и матчат любые латинские буквы.


## Экранирование и escape-последовательности {#jekranirovanieiescape-posledovatelnosti}

В теле выражения доступно экранирование с помощью символа `\` - любой символ, стоящий после обратного слэша будет представлен в теле выражения без изменений, кроме специальных escape-последовательностей, предназначенных для задания особых символов или классов символов:

- `\a` U+0007 Bell;
    
- `\b` U+0008 Backspace;
    
- `\t` U+0009 Horizontal Tab;
    
- ``\n`` U+000A Line Feed;
    
- `\v` U+000B Vertical Tab;
    
- `\f` U+000C Form Feed;
    
- `\r` U+000D Carriage Return;
    
- `\s` Класс пробельных (whitespace) символов;
    
- `\S` Класс не-пробельных символов (дополнение `\s`);
    
- `\w` Класс букв;
    
- `\W` Класс не-букв (дополнение `\w`);
    
- `\d` Класс цифр (в том числе экзотических);
    
- `\D` Класс не-цифр (дополнение `\d`).
    

Особым образом задается обратный слэш: `\\\\`.


## Классы символов {#klassysimvolov}

Класс символов задается в квадратных скобках и при матчинге соответствует одному символу из заданных в классе.

Пример: `[абв]` матчит любой из символов "а", "б" или "в".

При описании классов используются следующие конструкции:

- `[^...]` инвертированный класс (дополнение множества символов) матчит все символы, кроме заданных;
    
- `:name:` класс символов категории `name`;
    
- `X-Y` диапазон матчит любой символ из заданного диапазона Unicode-символов от x до y;
    
- `\X` escape-последовательность (см. [выше](#jekranirovanieiescape-posledovatelnosti));
    
- `\xNN` escape-последовательность, задающая символ с кодом U+00NN, где NN - шестнадцатеричное число;
    
- `\uNNNN` escape-последовательность, задающая символ с кодом U+NNNN, где NNNN - шестнадцатеричное число;
    
- `\UNNNNNNNN` escape-последовательность, задающая расширенный символ не из Basic Multilingual Plane с кодом U+NNNNNNNN, где NNNNNNNN - шестнадцатеричное число.
    

Примеры:

`[^абв]` - любой символ, кроме "а", "б" и "в".

`[а-я]` - любой символ в диапазоне от "a" (U+0430) до "я" (U+044F).

`[\t\n]` - таб или перенос строки.

`[\w\d]` - любая буква или цифра.

`[\j]` - символ "j".

`[\x4C]` - символ "L" (U+004C Latin Capital Letter L).

`[\u0426]` - символ "Ц" (U+0426 Cyrillic Capital Letter Tse).

`[\U00010481]` - символ "ҁ" (U+10481 Osmanya Letter Ba).

Классы могут вкладываться друг в друга.

Пример:

`[0-9[^\w\d]]` матчит традиционные цифры, а также все символы, не являющиеся буквами или цифрами.

