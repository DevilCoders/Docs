# Работа с почтой

1. Отправка сообщения на указанный адрес

```groovy
api.mail.send(HasGid owner, String to, String subject, String text)
api.mail.sendHtml(HasGid owner, String to, String subject, String text)
```
  Где:
   - owner - объект, в рамках которого отправляется письмо, например, тикет
   - to - адрес получателя, например, "pupkin@example.com" или "Пупкин <pupkin@example.com>"
   - subject - тема письма
   - text - тело письма
   
2. `api.mail.isValidOrEmptyEmail(email)` - проверяет email на соответствие RFC