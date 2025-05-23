# Tunneler

Tunneler – сервис, предоставляющий HTTPS over SSH туннели. Пригодится вам, если вы подняли некоторый стенд (например, развернули web4) локально, и хотите сделать его доступным с других устройств во внутренней сети Яндекса. Например, чтобы дизайнер мог посмотреть ваш стенд, или чтобы запустить hermione-тесты на вашем стенде. Аналог из внешнего мира — [ngrok](https://ngrok.com/).

## Принцип работы

Tunneler имеет несколько инсталляций, которые поддерживает Служба инфраструктуры фронтенда:

- `https://ws{1,2,3}-tunnelerapi.tunneler-si.yandex-team.ru/` для использования людьми
- `https://tun.si.yandex-team.ru/` для использования роботами в CI

При желании вы можете развернуть свою. Инструкций по разворачиванию нет, за помощью можно прийти в [INFRADUTY](https://wiki.yandex-team.ru/infraduty/form/).

Вот как работает использование tunneler через archon или templar:

1. npm-пакет (`@yandex-int/tunneler`) при запуске идёт в API tunneler (по урлу, к примеру, https://ws1-tunnelerapi.tunneler-si.yandex-team.ru/api/v1/instances) и получает список доступных инстансов в виде пар `host:port`.
2. Выбирает некоторый инстанс из этого списка и поднимает до него ssh-туннель, типа такого
  ```
  ssh -v -R 12345:<tunneler_instance>:3000 -N -p 2022 <tunneler_instance>
  ```
  Здесь 3000 — порт, на котором слушает ваше приложение локально; 12345 — случайно выбранный порт инстанса для поднятия туннеля; 2022 — порт, по которому происходит подкючение и авторизация — это порт из ответа API.
3. После этого по адресу `https://username-12345-ws1.tunneler-si.yandex.ru` вы можете увидеть ответ вашего стенда. Точный адрес залогируется в консоль.

## Использование в CI

Для CI используется инсталляция tunneler, отличная от той, что запускается локально. Ключевые отличия такие:

1. Список доступных инстансов отдаётся по урлу `https://tun.si.yandex-team.ru/api/v2/instances?cloud=yp`
2. Хосты у туннелей получаются вида `{dc}-{host}-{port}-yp.tun.si.yandex.ru` вместо туннелей по имени пользователя.

Поэтому клиент должен быть сконфигурирован под API v2 и подключаться к tun в YP. Проще всего для этого выставить env переменные:

```
tunneler_hosts='["tun.si.yandex-team.ru"]'
tunneler_version=2
tunneler_cloud=yp
```

Важно: все переменные должны быть установлены, в отдельности они не работают.
