## m-button-action

**Статус блока**: **deprecated**

Устарело, рекомендуется использовать библиотеку [staff-card](https://github.yandex-team.ru/tools/staff-card).

Кнопка, которая позволяет:

  * Позвонить на любой номер из внутренней телефонии.
  * Показать статус пользователя на внутреннем сервере jabber.
  * Написать в клиент jabber `xmpp:`.
  * Написать письмо `mailto:`.
  * Скопировать e-mail.

### Почта и jabber

```js
{
    block: 'm-button-action',
    mods: { type: 'email' },
    jabberSt: 'offline',
    content: 'ssyrkin@yandex-team.ru'
}
```

Для отрисовки статуса пользователя в jabber используется блок [mi-jabber](../mi-jabber/mi-jabber.ru.md).

### Телефония

```js
{
    block: 'm-button-action',
    mods: { type: 'phone' },
    content: '+38 (097) 123-45-67'
}
```

Для API телефонии используется блок [mi-phone-button](../mi-phone-button/mi-phone-button.ru.md).
