NotificationRow info

```(jsx)
<NotificationRowMarkdown type="info" onRequestClose={() => console.log('Do handleClose')}>
    {'Расскажите, как вы [работаете](#) с Метрикой — это займет пару минут [button:Пройти опрос](#)'}
</NotificationRowMarkdown>
```

NotificationRow update

```(jsx)
<NotificationRowMarkdown type="update" onRequestClose={() => console.log('Do handleClose')}>
    {'Обновлены правила [обеспечения](#) безопасности пользовательских данных [button:Ознакомиться](#)'}
</NotificationRowMarkdown>
```

NotificationRow critical

```(jsx)
<NotificationRowMarkdown type="critical" onRequestClose={() => console.log('Do handleClose')}>
    {'Ваш счетчик отключен. Такое случается, если с ним делать всякое. Не расстраивайтесь и просто сохраняте спокойствие. Скорее всего, вы не потеряете всех своих денег. Сделайте основное.\n\
    Зайдтите на счетчик и посмотрите на него. Деньги еще с вами? Тогда [подтвердите](#), что вы — это вы, а не кто-то там [button:Подтвердить](#) [button:Я ничего не делал](#)'}
</NotificationRowMarkdown>
```
