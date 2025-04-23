# waffles

Вафли - сервис для получения списка хостов по ip адресу.

## API

**Запрос:**

`https://waffles.sec.yandex.net/api/v1/virtual_host/2a02:6b8:0:3400::519`

**Ответ:**
```
{"2a02:6b8:0:3400::519":["molly.yandex-team.ru","sslrate.yandex-team.ru","sibtools.stable.qloud-b.yandex.net","ctf.yandex-team.ru","yadi-tst.yandex-team.ru","csp-tester.yandex-team.ru","debby.sec.yandex-team.ru","debby-test.sec.yandex-team.ru","yadi.yandex-team.ru","yodax.yandex-team.ru","reni.yandex-team.ru","*.sec.yandex-team.ru"]}
```
## WEB UI

`https://waffles.sec.yandex-team.ru/user/virtual_host/77.88.55.50`

## Аутентификация
Для аутентификации используется TVM2.0, заголовок X-Ya-Service-Ticket.

Dst id - 2008801.

Для добавления вашего приложения - напишите @a-abakumov
