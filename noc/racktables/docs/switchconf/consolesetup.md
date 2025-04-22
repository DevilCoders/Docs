# mpdaemon и все все все

Наливкой устройств через консольные порты занимается `multiportdaemon.rb`, более известный как "mpdaemon".  
Более подробно про наливку и взаимодействие mpdaemon с другими компонентами [тут](https://wiki.yandex-team.ru/azryve/nalivka-debug/)

## Основные запчасти

### `multiportdaemon.rb`

Обслуживает консольные порты, стоящие в наливке. До момента пока не сможет залогиниться на железку на консольном порту, ничего про нее не знает и не догадывается.
С RT связан очень просто: RT выгружает конфиг со списком портов в наливке в файл clf.conf и послылает демону `SIGHUP`, чтоб тот обновил свое понимание мира.

Для работы самого демона, наличие рядом RT - не обязательно. Но нужен доступ к консоляторам, на которых надо наливать железки.

### `process.rb`

Родной брат mpdaemon'a, часто используется для отладки и проверки изменений в наливке.
Требования для работы еще проще: нужен доступ к консоляторам, либо проброс консоли любым способом в файл-сокет.
Для использования достаточно запустить проверку в тестовой ветке(в стороне от продакшена) на серверах с доступом (как правило noc-sas/noc-myt):

```bash
cd switchconf
./process.rb --port fish:cuau0
```

Как и старший брат, использует MySerial.rb для доступа к консолям, поэтому может сам попасть на консолятор.
Для дебага можно передать произвольный файл конфига через агрумент `process.rb -f`. Тогда устройству подключенному к консоли, не обязательно быть назначенным в наливку.
Форсировать переустановку софта можно через аргумент `process.rb --force`.

### Возможные ошибки

`Permission denied @ rb_sysopen - /var/lock/LCK`: для запуска нужен `sudo` чтобы схватить файллок
```bash
$ ./process.rb -p consoles-red-lab:ttyS31
Permission denied @ rb_sysopen - /var/lock/LCK..consoles-red-lab:ttyS31
```

`Operation timed out - user specified timeout`: нужно проверить что консолятор доступен. При этом стоит помнить что у консолятора можеть быть более одного адреса.
```bash
$ sudo ./process.rb -p consoles-red-lab:ttyS31
Cleared stale lockfile /var/lock/LCK..consoles-red-lab:ttyS31
Operation timed out - user specified timeout
at /usr/local/lib/ruby/2.7/socket.rb:61:in `connect_internal'
```

`Could not attach to port on conserver`: на порту уже запущена наливка. Чтобы дебажить собственным истансом `process.rb` нужно ее выключить.
```bash
$ sudo ./process.rb -p consoles-red-lab.yndx.net:ttyS31
Cleared stale lockfile /var/lock/LCK..consoles-red-lab.yndx.net:ttyS31
Could not attach to port on conserver @ consoles-red-lab.yndx.net:ttyS31 (got '[spy]^J')
at /usr/home/azryve/src/rt/rt-yandex/switchconf/MySerial.rb:235:in `conserver_expect'
```

## Связь с RT

DeviceConfig.rb общается с RT через `export/getswitchconfig2.php`, получает конфиг, отправляет результат.
Модуль для наливки AP Aruba использует InvAPI для получения серийных номеров.


## Console cheatsheet

Подключиться к порту консолятора можно с любого нока запустив клиент `console`, аргументом дав ему имя хоста консолятора без префикса "consoles-", к которому через дефис добавлено имя порта:

```
$ console red-lab-ttyS31
/usr/bin/console> calling /usr/local/bin/console -n -p10101 -M 5.255.236.89 ttyS31
[Enter `^Ec?' for help]
[-- MOTD --
motd> ******************************************
motd> **** By default console speed is 9600 ****
motd> ******************************************
motd> Userful magic sequences:
motd>     ^E,c,s,u - Baud up: 9600->19200->38400->57600->115200
motd>     ^E,c,s,d - Baud down]
```

У `conserver` есть набор комбинаций клавиш позволяющих управлять подключением.

Все они начинаются с escape-последовательности `^E c`. Сначала жмем `Ctrl+e` (`e` на английской раскладке). Затем нажимаем `c` (уже без зажатого `Ctrl`).

Её нужно вводить чтобы консолятор понял что следующие за ним клавиши предназначаются ему, а не устройству подключенному к консоли.
Если она введена успешно - в консоли появится символ `[` и консоль начнет интерпритировать следующие символы.
Последющая комбинация может состаять как из одного, так и из несольких символов.

Наиболее полезные

```
^E c .      # отключиться от консоли и выйти из клиента
^E c f      # скинуть с консоли текущего пользователя и подключиться самому из spy-режима
^E c S      # переключиться в read-only режиме (spy mode) и пустить другого пользователя за консоль
^E c ?      # посмотреть на все доступные команды
^E c s u    # поднять скорость на консоли
^E c s d    # уменьшить скорость на консоли
^E c i      # посмотреть на информацию о текущих портах консолятора к которому подключен (скорость, flow-control, etc.)
^E c l 0    # SysRq, полезно для залипших вайтбоксов с линуксом. можно через R E I S U B ребутнуть даже самый зависший. sysrq нужно повторять перед каждым.
```

Полный список (вывод `^E c ?`)
```
 .       disconnect                     ;       move to another console
 a       attach read/write              b       send broadcast message
 c       toggle flow control            d       down a console
 e       change escape sequence         f       force attach read/write
 g       group info                     i       information dump
 L       toggle logging on/off          l?      break sequence list
 l0      send break per config file     l1-9a-z send specific break sequence
 m       display message of the day     n       write a note to the logfile
 o       (re)open the tty and log file  p       playback the last 60 lines
 P       set number of playback lines   r       replay the last 20 lines
 R       set number of replay lines     S       spy mode (read only)
 su      serial baud up                 sd      serial baud down
 sf      cycle through flow control (RTS/CTS, XON/XOFF, none)
 sy      cycle through parity settings (even, odd, none)
 u       show host status               v       show version info
 w       who is on this console         x       show console baud info
 z       suspend the connection         !       invoke task
 |       attach local command           ?       print this message
 <cr>    ignore/abort command           ^R      replay the last line
 \ooo    send character by octal code
```
