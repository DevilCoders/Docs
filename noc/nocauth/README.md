Сервис tacacs - реализация RFC 8907.

## Тестинг
Для тестинга подняты [сервера](https://c.yandex-team.ru/groups/nocauth-testing).
Чтобы их начать использовать, надо переключить сервера на один из них. Пример проверки доступность:
```
man1-s391# telnet 5.255.230.53 49 vrf management
Trying 5.255.230.53...
Connected to 5.255.230.53.
Escape character is '^]'.
```
Перед переключением убедись что на свитче есть локальная учетка.

## Диагностика:
tacacs протокол удобно читать в wireshark. Чтобы он смог декодировать пакеты, надо в настройках указать
tacacs секрет.

### nexus
На Nexus есть команда
```
man1-s391# show priv
```
```shell
User name: robot-gfglister-nocauth
Current privilege level: -1
Feature privilege: Enabled
```
privilege level: -1 - не отправлен priv от TACACS+-сервера.
### ASR
Priv можно посмотреть в debug tacacs
```
RP/0/RSP0/CPU0:Jul 11 14:35:28.332 : tacacsd[1138]: Privilege level callback for request 0x500453e8
RP/0/RSP0/CPU0:Jul 11 14:35:28.332 : tacacsd[1138]: priv-lvl = 2
```

```
RP/0/RSP0/CPU0:mar-arr1#show user all
Mon Jul 11 14:35:32.514 MSK
Username: robot-gfglister-nocauth
Authenticated using method tacacs+
User robot-gfglister-nocauth has the following Task ID(s):

No task ids available
```
