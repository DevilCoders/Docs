# OAuth-авторизация в Яндекс.Почте

Почтовые клиенты и приложения могут получать доступ к ящикам Яндекс.Почты по протоколу OAuth. Этот протокол позволяет программам не запрашивать и не хранить логины и пароли, а пользователям — не беспокоиться о безопасности паролей.

OAuth-авторизацию поддерживают IMAP- и SMTP-серверы Яндекс.Почты. Авторизация реализована с помощью механизма XOAUTH2, который также использует [Gmail](https://developers.google.com/gmail/xoauth2_protocol){% if lang == "ru" %} и [почта Mail.ru](https://oauth.mail.ru/docs/){% endif %}.

## Подключение {#quickstart}

Чтобы реализовать OAuth-авторизацию в своем почтовом клиенте:

1. [Зарегистрируйте приложение](../oauth/tasks/register-client.md) на Яндекс.OAuth со следующими правами:
    
   - для авторизации на SMTP-сервере — **Яндекс.Почта** → **Отправка писем через Яндекс.Почту по протоколу SMTP**;
   - для авторизации на IMAP-сервере — **Яндекс.Почта** → **Доступ на чтение писем в почтовом ящике** или **Чтение и удаление писем в почтовом ящике**.
    
1. Реализуйте запрос OAuth-токенов любым доступным способом (см. [документацию Яндекс.OAuth](../oauth/concepts/about.md)). Для первоначального тестирования можно использовать [отладочный токен](../oauth/tasks/get-oauth-token.md).
    
1. Организуйте отправку OAuth-токенов в Яндекс.Почту и обработку ответа сервера. Ниже описано корректное взаимодействие с серверами Яндекс.Почты по протоколам [IMAP](#imap) и [SMTP](#smtp).
    
### Адреса почтовых серверов {#addresses}

Обращаться к почтовым серверам следует по следующим адресам:

- IMAP-сервер — `imap.yandex.com:993`,
  
- SMTP-сервер — `smtp.yandex.com:465`.

## Взаимодействие с IMAP-сервером {#imap}

При авторизации на IMAP-сервере ваша программа должна использовать команду `AUTHENTICATE` с механизмом `XOAUTH2` (этот механизм не упоминается в выводе команды `CAPABILITY`, но поддерживается). OAuth-токен и email пользователя следует передавать в аргументе команды.

Чтобы составить аргумент с авторизационными данными:

1. Подготовьте строку с данными:

   ```no-highlight
   user=<логин>\@yandex.\001auth=Bearer <OAuth-токен>\001\001
   ```

1. Закодируйте полученную строку методом base64, например:
    
   ```no-highlight
   dXNlcj10ZXN0QHlhbmRleC5ydQFhdXRoPUJlYXJlciBBcmRGZmlnQUFLRndFVWJwWnExRlF4dWZ3SmxycS1wRTJnAQE=
   ```

Команда `AUTHENTICATE` должна быть оформлена как одна строка, без разрывов и переносов (пример ниже отформатирован для удобства чтения). Последовательность запросов и ответов при успешной IMAP-авторизации может выглядеть так:

```no-highlight
openssl s_client -connect imap.yandex.com:993 -crlf

<инициализация соединения>

клиент: C01 CAPABILITY
сервер: * CAPABILITY IMAP4rev1 CHILDREN UNSELECT LITERAL+ NAMESPACE XLIST BINARY UIDPLUS ENABLE ID AUTH=PLAIN IDLE MOVE
сервер: C01 OK CAPABILITY Completed.
клиент: A01 AUTHENTICATE XOAUTH2 dXNlcj10ZXN0QHlhbmRleC5ydQFhdXRoPUJlYXJlciBBcmRGZmlnQUFLRndFVWJwWnExRlF4dWZ3SmxycS1wRTJnAQE=
сервер: * CAPABILITY IMAP4rev1 CHILDREN UNSELECT LITERAL+ NAMESPACE XLIST BINARY UIDPLUS ENABLE ID IDLE MOVE
сервер: A01 OK AUTHENTICATE Completed.

<продолжение работы>
```

### Ответ об ошибке авторизации {#imap-error}

Сервер возвращает описание ошибки в ответ на команду `AUTHENTICATE`. Последовательность запросов и ответов с ошибкой IMAP-авторизации может выглядеть так:

```no-highlight
openssl s_client -connect imap.yandex.com:993 -crlf

<инициализация соединения>

клиент: C01 CAPABILITY
сервер: * CAPABILITY CHILDREN UNSELECT LITERAL+ NAMESPACE XLIST BINARY UIDPLUS ENABLE ID AUTH=PLAIN IDLE MOVE
сервер: C01 OK CAPABILITY Completed.
клиент: A01 AUTHENTICATE XOAUTH2 dXNlcj10ZXN0MUB5YW5kZXgucnUBYXV0aD1CZWFyZXIgQXJkRmZpZ0FBS0Z3RVVicFpxMUZReHVmd0pscnEtcEUyZwEB
сервер: A01 NO [AUTHENTICATIONFAILED] AUTHENTICATE Invalid credentials or IMAP is disabled sc=ANQhQk2BrGkH_101523_7m

<продолжение работы>
```

После описания ошибки сервер приводит последовательность вида `sc=ANQrQk2BrGkH_101523_7m`. Это идентификатор сессии, который стоит указать, если вы обращаетесь с этой ошибкой в службу поддержки Яндекс.Почты.

## Взаимодействие с SMTP-сервером {#smtp}

При авторизации на SMTP-сервере ваша программа должна использовать команду `AUTH` с механизмом `XOAUTH2`. Токен и логин пользователя следует закодировать и передавать в аргументе команды.

Аргумент с авторизационными данными составляется так же, как и для протокола IMAP:

1. Подготовьте строку с данными:
    
   ```no-highlight
   user=<логин>\@yandex.\001auth=Bearer <OAuth-токен>\001\001
   ```
    
1. Закодируйте полученную строку методом base64, например:
    
   ```no-highlight
   dXNlcj10ZXN0QHlhbmRleC5ydQFhdXRoPUJlYXJlciBBcmRGZmlnQUFLRndFVWJwWnExRlF4dWZ3SmxycS1wRTJnAQE=
   ```

Последовательность запросов и ответов при успешной SMTP-авторизации выглядит так:

```no-highlight
openssl s_client -connect smtp.yandex.com:465 -crlf

<инициализация соединения>

сервер: 220 smtp2o.mail.yandex.net ESMTP (Want to use Yandex.Mail for your domain? Visit http://pdd.yandex.ru)
клиент:EHLO sender.example.com
сервер:250-smtp2o.mail.yandex.net
сервер:250-8BITMIME
сервер:250-PIPELINING
сервер:250-SIZE 42991616
сервер:250-AUTH LOGIN PLAIN XOAUTH2
сервер:250-DSN
сервер:250 ENHANCEDSTATUSCODES
клиент:AUTH XOAUTH2 dXNlcj10ZXN0QHlhbmRleC5ydQFhdXRoPUJlYXJlciBBcmRGZmlnQUFLRndFVWJwWnExRlF4dWZ3SmxycS1wRTJnAQE=
сервер:235 2.7.0 Authentication successful.

<продолжение работы>
```

Команда `AUTH` должна быть оформлена как одна строка, без переносов (пример отформатирован для удобства чтения).

### Ответ об ошибке авторизации {#smtp-error}

Сервер возвращает описание ошибки в ответ на команду `AUTH`, с кодом 535.

Пример последовательности запросов и ответов при ошибке SMTP-авторизации:

```no-highlight
openssl s_client -connect smtp.yandex.com:465 -crlf

<инициализация соединения>

сервер: 220 smtp2o.mail.yandex.net ESMTP (Want to use Yandex.Mail for your domain? Visit http://pdd.yandex.ru)
клиент:EHLO sender.example.com
сервер:250-smtp2o.mail.yandex.net
сервер:250-8BITMIME
сервер:250-PIPELINING
сервер:250-SIZE 42991616
сервер:250-AUTH LOGIN PLAIN XOAUTH2
сервер:250-DSN
сервер:250 ENHANCEDSTATUSCODES
клиент:AUTH XOAUTH2 dXNlcj10ZXN0MUB5YW5kZXgucnUBYXV0aD1CZWFyZXIgQXJkRmZpZ0FBS0Z3RVVicFpxMUZReHVmd0pscnEtcEUyZwEB
сервер:535 5.7.8 Error: authentication failed: Invalid user or password!

<продолжение работы>
```

Если авторизационная строка была составлена неверно, ошибка будет такой:

```no-highlight
сервер: 535 5.7.8 Error: authentication failed:Invalid format.
```
