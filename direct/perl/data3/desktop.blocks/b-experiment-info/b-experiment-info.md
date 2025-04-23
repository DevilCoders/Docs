# b-experiment-info

Блок с информацией об эксперименте (AB-тестирование) с кнопкой "Остановить"

### Автор 
[dima117a](https://staff.yandex-team.ru/dima117a)

Пример:
```
{ 
    block: 'b-experiment-info', 
    exp: {
        experimentId: 123,
        from: '2016-07-21',
        to: '2016-08-05',

        cid1: '7162548',
        name1: 'Моя первая кампания',

        cid2: '87235628',
        name2: 'Моя вторая кампания',

        percent: 70 // процент аудитории для кампании A   
    }
}
```
