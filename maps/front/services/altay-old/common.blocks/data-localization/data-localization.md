### API
#### joinTranslations
Соединяет переводы по одинаковым локалям
##### example
Есть исходный массив переводов:
```
[
    { locale: 'en', value: 'tr1' }, 
    { locale: 'en', value: 'tr2' }, 
    { locale: 'en', value: 'tr3' }, 
    { locale: 'ru', value: 'пр1' }
]
```

Нам необходимо получить все переводы по каждой из локалей, для этого вызываем следующее:

```
const translations = [/* исходный массив переводов */];
const localization = this.dataLocalization(userLocale, pageLocale);

translations = localization.joinTranslations(translations);
```

На выходе массив будет выглядеть вот так:

```
[
    { locale: 'en', value: ['tr1', 'tr2', 'tr3'] },
    { locale: 'ru', value: ['пр1'] }
]
```
