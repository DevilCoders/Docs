Именование блоков
=================

Есть основные блоки (поставляются пользователям) и вспомогательные
блоки (используются в примерах и тестах).

Имена любых блоков пишутся строчными буквами,
в качестве разделителей слов используются дефис:


```js
// Правильно
button
country-flag

// Неправильно
Block
countryFlag
```

В основных блоках также не используются префиксы:
```js
// Неправильно
b-button
```

Во вспомогательных блоках префиксы допустимы.

## Новые версии блоков

При внесении обратно несовместимых изменений создается новый блок.
Новая версия блока делается под тем же именем, но в конце добавляется число начиная с 2.

```js
button
button2
button3
```
