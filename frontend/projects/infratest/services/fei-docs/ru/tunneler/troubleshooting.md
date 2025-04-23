# Troubleshooting

В этом разделе покажем, как самостоятельно разобраться с ошибками подключения tunneler.

Самый простой способ найти ошибку — запустить приложение с переменной окружения `DEBUG=ssh-tun`. Например, если вы запускаете сервер разработки так:

```
npx archon kotik --public
```

попробуйте запустить:

```
DEBUG=ssh-tun npx archon kotik --public
```

Так вы увидите в консоли сырые логи от ssh-клиента. В них можно найти более точную ошибку, например, об отсутствующем ssh-ключе. Если чтение лога не помогло, двигайтесь дальше.

Выясните, поднимаются ли туннели у коллег из вашей группы или вашего сервиса. Если у них всё в порядке, то проблема может скрываться в вашей конфигурации. Если туннели не поднимаются у всей команды, вероятно, у всей вашей группы просто нет [доступов](./access.md).

Если доступы есть, а туннели не поднимаются, проведите описанный ниже анализ самостоятельно, чтобы локализовать проблему.

## Туннель поднимается, но в браузере только No such tunnel

Может быть связано с тем, что для подключения используются устаревшие (и оторванные) домены `ws{n}-tunnelerapi.si.yandex-team.ru`. Убедитесь, что переменная `TUNNELER_HOST` не используется.

## У вас skotty и куча кастомных правил в .ssh/config
Добавьте в ```.ssh/config``` правило:
```
Host 2a02:6b8:*
    ForwardAgent ~/.skotty/sock/sudo.sock
    IdentityAgent ~/.skotty/sock/default.sock
```

## Бета открывается с компьютера, но с iPhone по VPN не грузится

Под VPN на iOS по умолчанию отключен IPv6. Напишите на [help@yandex-team.ru](mailto:help@yandex-team.ru) чтобы накатили IPv6 в вашу конфигурацию VPN.

## Браузер жалуется на сертификат

Ошибка вида "cert invalid authority". Текст может различаться от браузера к браузеру.
Скорее всего, в браузере не установлен внутренний сертификат. [Установите его](https://wiki.yandex-team.ru/security/ssl/sslclientfix/).

## Туннель не поднимается

Если у вас проблемы, отличные от проблем выше, например такие:

```
ERROR: failed to create tunnel after 5 attempts
```

то приготовьтесь к расследованию. Сохраняйте логи всех команд, и в случае неудачного расследования загружайте их на [Yandex Paste](https://paste.yandex-team.ru/), чтобы приложить к обращению в поддержку.

### Проверка окружения

Важно: эти команды необходимо выполнять на той же машине, с которой вы пытаетесь подключиться. И в том же окружении: если вы используете tmux/screen, выполняйте команды из него.

1. Сперва проверьте, что у вас корректно работает IPv6 во внутренней сети. Ошибки вида
  ```
  { [RequestError: connect EHOSTUNREACH <ip>:443 - Local (:::60101)]
    code: 'EHOSTUNREACH',
    message: 'connect EHOSTUNREACH <ip>:443 - Local (:::60101)',
    host: 'ws1-tunnelerapi.si.yandex-team.ru',
    hostname: 'ws1-tunnelerapi.si.yandex-team.ru',
    method: 'GET',
    path: '/api/v1/instances' }
  ```
  выглядят как проблема с конфигурацией сети. Убедиться в этом можно, например, так:
  ```bash
  ping6 -c 4 staff.yandex-team.ru
  # В случае проблем с сетью пинги проходить не будут
  ```
  Если вы находитесь в офисе, попробуйте запускать tunneler как с VPN, так и без VPN — могут быть ошибки в конфигурации офисной сети или VPN.

  Если у вас Windows и вы используете WSL2, то там IPv6 [не завезли](https://docs.microsoft.com/ru-ru/windows/wsl/compare-versions#ipv6-access). Используйте WSL1.

2. Убедитесь, что у вас в hosts нет записей про хосты со словами `tunneler` или `tun`:
  ```bash
  # Для mac и linux
  cat /etc/hosts
  ```
  Для Windows проверьте содержимое файла `%WinDir%\System32\Drivers\Etc\Hosts`.

3. Проверьте, что у вас нет переменных окружения про Tunneler:
  ```bash
  env | grep -i tun
  ```

4. Наконец, удостоверьтесь, что у вас корректно настроены SSH-ключи:
  ```bash
  ssh -v arcadia.yandex.ru
  # Если ключ подошёл, вывод команды будет содержать строку
  # Authentication succeeded (publickey)
  ```
  Если вы эту строку не видите, настройте ваши SSH-ключи и SSH-agent [по инструкции](https://wiki.yandex-team.ru/security/ssh/#instrukciiponastrojjkessh-klientov). После настройки снова проверьте подключение вышеуказанной командой.

  :open_book: Если вы используете [skotty](https://docs.yandex-team.ru/skotty/ssh-client) и запускаете Tunneler с удалённого сервера, убедитесь, что в `~/.ssh/config` для этого сервера у вас включён форвардинг default-сокета, а не sudo: `ForwardAgent ~/.skotty/sock/default.sock`.

### Доступы к Tunneler API

Попробуйте вручную получить список доступных инстансов:

```bash
curl https://ws3-tunnelerapi.tunneler-si.yandex-team.ru/api/v1/instances
```

Корректный ответ выглядит примерно так (хост и порт могут отличаться)

```json
["ukwcrvctwg4w3ivt.sas.yp-c.yandex.net:2022"]
```

Если получили корректный ответ, переходите к проверке [доступов к инстансам](#dostupy-do-instansov-tunneler).

Вместо корректного ответа вы можете получить ошибку:

```
curl: (7) Failed to connect to ws3-tunnelerapi.tunneler-si.yandex-team.ru port 443: Connection timed out
```

Ошибка, как правило, свидетельствует об отсутствии дырки (сетевого доступа) до балансера Tunneler. Проверить и заказать дырку можно [по инструкции](./access.md).

### Доступы до инстансов Tunneler

Чтобы поднять туннель, необходим ssh-доступ до инстансов Tunneler.

Перед расследованием:

1. Если вы находитесь в офисе, попробуйте запускать tunneler как с VPN, так и без VPN — могут быть ошибки в конфигурации офисной сети или VPN.
2. Выполните `pkill -f "ssh"` если у вас есть подвисшие туннели.
3. Убедитесь, что выключено сжатие в `~/.ssh/config` (`Compression no` или параметр не указан).

Теперь расследование. Получите список доступных инстансов:

```bash
curl https://ws3-tunnelerapi.tunneler-si.yandex-team.ru/api/v1/instances
```

Ответ будет вроде такого:

```json
["zmbjt6yjwlhhvcsf.vla.yp-c.yandex.net:2022"]
```

Значит доступный адрес инстанса — хост `zmbjt6yjwlhhvcsf.vla.yp-c.yandex.net` и порт `2022`. Попробуйте подключиться к нему по ssh с verbose-логами:

```bash
ssh -vvv zmbjt6yjwlhhvcsf.vla.yp-c.yandex.net -p 2022
# В случае успешного подключения вывод команды будет содержать строку
# Authentication succeeded (publickey)
```

Вместо корректного ответа вы можете получить одну из ошибок:

```
ssh: connect to host zmbjt6yjwlhhvcsf.vla.yp-c.yandex.net port 2022: Operation timed out
```
```
ssh: connect to host zmbjt6yjwlhhvcsf.vla.yp-c.yandex.net port 2022: Permission denied
```


Ошибка, как правило, свидетельствует об отсутствии дырки (сетевого доступа) до самих инстансов Tunneler. Проверить и заказать дырку можно [по инструкции](./access.md).

Если доступ есть (вы видите `Authentication succeeded`), а туннель не поднимается, напишите на [INFRADUTY](https://wiki.yandex-team.ru/infraduty/form/), приложив текстовые логи всех выполненных команд.

Если доступа нет, поищите в выводе команды такие строки:

```
Trying private key: /path/to/.ssh/id_rsa
```

Здесь `/path/to/.ssh/id_rsa` должно соответствовать расположению вашего приватного ключа, к примеру `/Users/<username>/.ssh/id_rsa`. Если вы видите, что предлагается не тот ключ, проверьте его наличие в ssh-agent:

```
ssh-add -l
```

Команда должна отобразить ваш ключ, в противном случае выполните:

```
ssh-add -K /path/to/my_key
```

и попробуйте подключиться вновь. Не помогло — попробуйте с пустым `~/.ssh/config`.

Используете tmux/screen? Проверьте, что [он дружит с ssh-agent](https://wiki.yandex-team.ru/security/ssh/linux/#agentforwardingscreen/tmux).

Если вы не смогли самостоятельно локализовать и починить проблему, пишите в [INFRADUTY](https://wiki.yandex-team.ru/infraduty/form/). К сообщению приложите логи всех команд, которые вы выполняли для расследования. Как можно подробнее опишите своё окружение.

### Проблемы с доступом из VirtualBox

Настройте на виртуальной машине IPv6 [по инструкции](https://wiki.yandex-team.ru/q/devops/faq/ipv6-virtual-box/#nastroitipv6).

### Во всех остальных случаях

Напишите на [INFRADUTY](https://wiki.yandex-team.ru/infraduty/form/).
