Показывает блок опроса с возможностью перехода между несколькими вопросами.
По событию onEnd отдает результаты опроса. Скрытие блока ответственность 
родительского компонента.

Пример использования:
```jsx
const steps = [
    {
        question: 'Столица Бразилии?',
        options: [{
                label: 'Бразилия', value: '1',
            }, {
                label: 'Бразилиа', value: '2',
            },
        ],
        multi: true,
    }, {
        question: 'А столица Мексики?',
        options: [{
                label: 'Мексика', value: '1',
            }, {
                label: 'Мехико',  value: '2',
            },
        ],
        multi: false,
    },
]

<Poller
    steps={steps}
    onEnd={val => console.log(val)}
    showEndButton={true}
/>
```
