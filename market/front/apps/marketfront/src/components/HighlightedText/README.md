# Marketplace

Компонент для отображения подсвеченных слов/фрагментов слов из запроса.
Можно использовать в следующих случаях:
1) репорт в ответ на неверно набранное слово возвращает в поле spellchecker информацию об ошибке и фрагменты
слов, которые нужно выделить, в поле highlighted
2) в ответ на запрос в поле titles>highlighted товара будут отмечены слова из запроса, если они в этом заголовке есть

```jsx
<HighlightedText
    text={{
        raw: 'Очепатка',
        highlighted: [
            {value: 'О'},
            {value: 'чеп', highlight: true},
            {value: 'атка'},
        ]
    }}
/>
```
