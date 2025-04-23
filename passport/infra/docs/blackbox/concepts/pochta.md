# Поиск учетной записи по e-mail

Вызывая методы [login](../methods/login.md) и [userinfo](../methods/userinfo.md), вы можете идентифицировать пользователя по e-mail, передав адрес электронной почты в значении аргумента `login`. Передавать можно следующие адреса:

- Созданные при заведении почтового ящика Яндекса (<логин>@yandex.ru, <логин>@yandex.com.tr и т. д.).
- Адрес на внешнем сервисе, указанный в качестве логина при регистрации лайт-пользователя.
- Адрес пользователя ПДД или алиас пользователя ПДД.

По дополнительным адресам, привязанным через [интерфейс Яндекс.Паспорта](https://passport.yandex.ru/profile/emails), пользователя найти нельзя.

## Поиск по почтовому ящику на Яндексе

Поиск по логину `username` и поиск по емейлу `username@yandex.ru` это не одно и то же.
Пользователь с таким логином может существовать, а почтовый ящик - нет.
Почтовый ящик на Яндексе может быть удален пользователем или заморожен, в этом случае почта в него не доставляется и по емейлу такой пользователь найден не будет.
Более того, логин `username` и емейл `username@yandex.ru` могут принадлежать разным аккаунтам и разным людям (см. следующий раздел).

## Область поиска e-mail

Адреса с одинаковой логиновой частью (например, `user@yandex.ru` и `user@narod.ru`) могут принадлежать разным пользователям. Также возможны коллизии между адресами ПДД и адресами лайт-аккаунтов.

Чтобы уточнять область поиска пользователя по e-mail, указывайте аргумент `sid`. Если аргумент не задан, ЧЯ использует значение по умолчанию, `sid=passport`.

### Значения аргументов sid

#### passport

Позволяет использовать алгоритм поиска электронного адреса, введенного в поле **логин** в домике при веб-авторизации.

ЧЯ ищет емейл следующим образом:
1. Берется доменная часть введенного адреса
1. Если этот домен принадлежит Яндексу (например, `yandex.ru`, `narod.ru`, `ya.ru` и т.д.), ЧЯ ищет логиновую часть емейла
   * среди алиасов типа `narodmail` или `portal`, если домен `@narod.ru`
   * среди алиасов типа `altdomain` если это альтернативный домен Яндекса, например, `galatasaray.net`
   * среди алиасов типа `phonenumber` если логин содержит цифры и не содержит букв
   * среди алиасов типа `mail` или `portal` в остальных случаях
1. Если домен не найден в списке доменов Яндекса, но передан [`sid=mk`](#mk), емейл ищется среди алиасов типа `lite`
1. Домен ищется в списке ПДД доменов и если есть такой домен, то логин ищется среди алиасов типа `pdd` и `pddalias`
1. Если домен не найден в списке ПДД и sid равен passport или не задан, то емейл ищется среди алиасов типа `lite`
1. Иначе считается, что емейл не найден.

В частности, отсюда следует, что ПДД пользователи имеют более высокий приоритет над лайт пользователями и в случае конфликта (один и тот же емейл у лайт пользователя и ПДД) будет выбираться аккаунт ПДД.

--------
#### smtp {#smtp}

Используется при обслуживании SMTP-соединений.

ЧЯ ищет логиновую часть e-mail среди алиасов типа `mail` или `portal` для адресов на домене Яндекса, либо среди алиасов `pdd` и `pddalias` для адресов на ПДД домене.
Для ПДД доменов работает логика выбора ящика по-умолчанию - если такого пользователя в домене нет, выбирается аккаунт, назначенный ящиком по-умолчанию для данного домена.

Для найденного аккаунта проверяется, что у него есть действующий почтовый ящик в Яндекс.Почте, т.е. что исходный e-mail действительно существует.

#### pop {#pop}

Используется при обслуживании POP3-соединений.

ЧЯ ищет логиновую часть e-mail среди алиасов типа `mail` или `portal` для адресов на домене Яндекса, либо среди алиасов `pdd` и `pddalias` для адресов на ПДД домене.
Выбор ящика по-умолчанию не работает.

Для найденного аккаунта проверяется, что у него есть действующий почтовый ящик в Яндекс.Почте, т.е. что исходный e-mail действительно существует.


#### mk {#mk}

Исторически, значение предназначалось для авторизации пользователей сервиса МойКруг (отсюда и название).
Сейчас оно позволяет отдать приоритет лайт-аккаунту в случае если переданный e-mail является одновременно и `lite`-алиасом и `pdd`-алиасом для разных аккаунтов.

Ниже приведены примеры использования e-mail в качестве логина в запросах к ЧЯ.


## Аутентификация пользователя {#pdd-userinfo-example}

Требуется проверить аутентификацию пользователя по логину и паролю, используя электронный адрес в качестве логина.

### Запрос {#pdd-userinfo-example}

```
wget -qO — 'https://blackbox.yandex.net/blackbox?method=login&login=motto22@yandex.ru&sid=pop&password=qwerty
&dbfields=accounts.login.uid,subscription.login.16&userip=194.84.46.241'
```

### Ответ с результатом аутентификации {#pdd-userinfo-example}

```
<?xml version="1.0" encoding="utf-8"?>
<doc>
  <status id="0">VALID</status>
  <error>OK</error>
  <uid hosted="0" domid="" domain="">7039392</uid>
  <login>motto22</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
  <dbfield id="accounts.login.uid">motto22</dbfield>
  <dbfield id="subscription.login.16">error-maker</dbfield>
  <password_quality>0</password_quality>
</doc>
```

## Получение информации о пользователе Почты для доменов {#pdd-userinfo-example}

Требуется получить базовую информацию о пользователе Почты для доменов и его логин, используя метод [userinfo](../methods/userinfo.md).

### Запрос

```
https://blackbox.yandex.net/blackbox?method=userinfo&login=pdd@okna.ru&sid=smtp&userip=194.84.46.241 
&dbfields=subscription.login.2'
```
Сервис получает следующий ответ:
### Ответ с информацией о пользователе

```
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <uid hosted="1" domid="1" domain="okna.ru" mx="0">1130000000001344</uid>
  <login>pdd</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
  <dbfield id="subscription.login.2">pdd@okna.ru</dbfield>
</doc>
```

### Ответ для несуществующего пользователя

Если пользователя не получается найти по указанному электронному адресу, сервис получает следующий ответ:
```
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <uid hosted="0"></uid>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
</doc>
```

### Ответ для существующего домена и несуществующего пользователя

Если указанный домен был найден, но на этом домене не получается найти пользователя, сервис получает следующий ответ:

```
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <uid hosted="1" domid="1" domain="okna.ru" mx="0" domain_ena="1" catch_all="0"></uid>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
</doc>
```


## Адреса с одинаковой логиновой частью {#auth-example}

Требуется получить логины пользователей, владеющих электронными адресами с одинаковой логиновой частью на @narod.ru и @yandex.ru.

### Запрос для @narod.ru

```
wget -qO — 'https://blackbox.yandex.net/blackbox/?method=userinfo&login=motto22@narod.ru&sid=pop&userip=194.84.46.241 
&dbfields=subscription.login.2,subscription.login.16'
```

### Ответ для @narod.ru

Логины пользователя, владеющего адресом motto22@narod.ru, в Почте (SID 2) и на Народе (SID 16) — «motto22» и «error-maker» соответственно.

```
<?xml version="1.0" encoding="utf-8"?>
<doc>
  <uid hosted="0" domid="" domain="">8740309</uid>
  <login>error-maker</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
  <dbfield id="subscription.login.16">motto22</dbfield>
  <dbfield id="subscription.login.2">error-maker</dbfield>
</doc>
```

### Запрос для @yandex.ru

```
wget -qO — 'https://blackbox.yandex.net/blackbox/?method=userinfo&login=motto22@yandex.ru&sid=pop&userip=194.84.46.241
&dbfields=subscription.login.2,subscription.login.16'
```

### Ответ для @yandex.ru

Логины пользователя, владеющего адресом motto22@yandex.ru, в Почте (SID 2) и на Народе (SID 16) — «error-maker» и «motto22» соответственно.
```
<?xml version="1.0" encoding="utf-8"?>
<doc>
  <uid hosted="0" domid="" domain="">7039392</uid>
  <login>motto22</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
  <dbfield id="subscription.login.16">error-maker</dbfield>
  <dbfield id="subscription.login.2">motto22</dbfield>
</doc>
```

