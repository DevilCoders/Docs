NotificationRow info

```(jsx)
const { Link } = require('lego');

<NotificationRow
    type="info"
    onRequestClose={() => console.log('Do handleClose')}
    buttons={[
        {
            text: 'Пройти опрос',
            url: '#',
            onButtonClick: () => console.log("Button was clicked: \'Пройти опрос\'"),
        },
    ]}
>
    Расскажите, как вы <Link theme="normal" url="#">работаете</Link> с Метрикой — это займет пару минут
</NotificationRow>
```

NotificationRow update

```(jsx)
const { Link } = require('lego');

<NotificationRow
    type="update"
    onRequestClose={() => console.log('Do handleClose')}
    buttons={[
        {
            text: 'Ознакомиться',
            url: '#',
            onButtonClick: () => console.log("Button was clicked: \'Ознакомиться\'"),
        },
    ]}
>
    Обновлены правила <Link theme="normal" url="#">обеспечения</Link> безопасности пользовательских данных
</NotificationRow>
```

NotificationRow critical

```(jsx)
const { Link } = require('lego');

<NotificationRow
    type="critical"
    onRequestClose={() => console.log('Do handleClose')}
    buttons={[
        {
            text: 'Подтвердить',
            url: '#',
            onButtonClick: () => console.log("Button was clicked: \'Подтвердить\'"),
        },
        {
            text: 'Я ничего не делал',
            url: '#',
            onButtonClick: () => console.log("Button was clicked: \'Я ничего не делал\'"),
        },
    ]}
>
    Ваш счетчик отключен. Такое случается, если с ним делать всякое. Не расстраивайтесь и просто сохраняте спокойствие. Скорее всего, вы не потеряете всех своих денег. Сделайте основное.<br/>
    Зайдтите на счетчик и посмотрите на него. Деньги еще с вами? Тогда <Link theme="normal" url="#">подтвердите</Link>, что вы — это вы, а не кто-то там
</NotificationRow>
```
