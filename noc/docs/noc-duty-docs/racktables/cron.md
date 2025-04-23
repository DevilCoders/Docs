# Racktables Crons

Логи Racktables cron лежат тут: `/var/log/rtcronsh`

### Cron: racktables-port-descriptions

#### Ошибка: Connection reset by peer at ./telnet line 118

**Причина** 

Racktables не может зайти на устройство по telnet.

**Решение**

Сдать дежурным NOC

### Cron: mac-learning-handler

Смотрит количество mac-адресов на порту и триггерит алерт в случае превышения допустимого значения mac-адресов на порту коммутатора.

#### Ошибка: These ports have too many learned MACs:

**Причина**

На порту обнаружено слишком много mac-адресов

**Решение**

1. Грепаем log
   ```
    [vdvolovik@noc-myt /var/log/rtcronsh/mac-learning-handler.php_check]$ cat 22-06-24T12-00-00.019MSK/stderr 
    ERROR: These ports have too many learned MACs:

    vla1-2s169 ge1/0/2 - 12276 MACs

    Consider disable mac learning notification traps on these ports
   ```
2. Самостоятельно или с помощью дежурного NOC узнаем что за устройство подключено к коммутатору
3. Сдаем проблему админу сервера
  - Пример: <https://st.yandex-team.ru/MACFARM-586>
