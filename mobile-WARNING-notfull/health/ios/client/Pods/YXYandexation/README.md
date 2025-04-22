# YXYandexation

Категория `YXYandexation` у `NSAttributedString` сделает вашу `NSAttributedString` в стиле Яндекс: Первая буква красная, оставшаяся часть строки — чёрная. 

Пример использования:

```objectivec
    NSAttributedString *string = [[NSAttributedString alloc] initWithString:@"Яндекс"];
    NSAttributedString *yandexated = [string yandexatedString];
```

Если же вам необходимо настроить размер и семейство шрифта, то вариант использования будет таким:

```objectivec
    NSMutableAttributedString *mutableString = [[NSMutableString alloc] initWithString:@"Яндекс" attributes:myAttributes];
    NSAttributedString *yandexated = [string yandexatedString];
```

При желании, вы можете яндексировать только первую букву текста

```objectivec
    NSAttributedString *string = [[NSAttributedString alloc] initWithString:@"Яндекс"];
    NSAttributedString *yandexated = [string stringByYandexatingFirstLetter];
```
