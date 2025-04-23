# Процедура добавления локальной учетки на сервера Racktables

## Назначение
Инструкция по добавлению локальной учетки на FreeBSD-шные сервера Racktables. Обычно это требуется для нового сетевого инженера, которому нужен доступ до любого оборудования и в gitlab.

Целевая аудитория данной инструкции - NOCDEV и сопричастные люди, имеющие sudo на серверах Racktables.


## TLDR

* Запускаем на мастере скрипт `/usr/local/rt-yandex.git/scripts/add-freebsd-user.sh`
* Просим пользователя сделать на мастере `passwd`
* Создаем учетку в [Racktables -> Local Users](https://racktables.yandex-team.ru/index.php?page=perms)
* Добавляем пользователя в [lusettings.php](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/blob/master/scripts/localuser-db/lusettings.php)
* Добавляем `<username>;<ssh-key>` в CVS `noc/routers/conffiles/pubkeys`
* Форсим выкатку на слейв через  `php /usr/local/rt-yandex.git/scripts/localuser-db/localuser-db.php -l<user> <slave>`
* Если нужны хеши для железок читаем [{#T}](gen-hashes.md)


## Создаем новую локальную UNIX-учетку на мастере Racktables
Найти мастера Racktables можно вот так
```
$ curl -G --data-urlencode "text=[мастер RT]" https://ro.racktables.yandex-team.ru/export/allobjects.php
noc-myt.yandex.net
```

На серверах FreeBSD все пользовательские учетные записи - локальные. Эти локальные учетные записи выкатываются на устройства, которым нужна локальная аутентификация. Синхронизация происходит с текущего мастера Racktables, поэтому добавлять пользователя надо на нем.

При создании учетной записи нового пользователя мы предполагаем, что

* коллега уже есть на стаффе
* он загрузил на него свои ssh-ключи
* у вас есть sudo на сервере Racktables

Создание происходит в полуручном режиме скриптом `/usr/local/rt-yandex.git/scripts/add-freebsd-user.sh`
* Заходим на мастер RT(не забудьте про SSH Agent, наши ключи нужны для секретницы)
* Запускаем скрипт передавая ему имя нового пользователя
* Переходим по ссылке и копипастим в промпт json с ssh-ключами со стаффа (ввод не отображается)
* Скрипт попросит проверить введенные данные, если все ок жмем 'y'


Что cделает скрипт после этого
* Создаст пользователя с нужным UID
* Распарсит json скопипащенный из staff и положит ключи в `.ssh/authorized_keys`
* Создает временный пароль из `pwgen` и кладет его в секретницу


Пример запуска
```
[azryve@noc-sas ~/src/rt/rt-yandex]$ ./scripts/add-freebsd-user.sh  robot-checkist
https://staff.yandex-team.ru/profile-api/ssh-keys/robot-checkist
Please open a URL and copy/paste JSON data
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

Добавяем пользователя: robot-checkist, uid: 4129
Добавляем в .ssh/authorized_keys: /tmp/add-freebsd-keys.7x2X1Slq (1 lines)
Временный пароль: es7aif4aizei4Aex

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

Continue? [y/n]:
y
Добавлям пользователя...done
Добавляем ключи в authorized_keys...done
Сохраняем пароль в секретнице...https://yav.yandex-team.ru/secret/sec-01fhdqxe273wqswzvkke2hvmq5
```

## Просим пользователя сменить пароль на мастере
Добавив пользователя на сервер просим пользователя

* Зайти по ssh на сервер на котором только что выполнили скрипт
* Выполнить `passwd` и заменить временный пароль на собственный

Важно помнить, что аутентификация на серверах Racktables - **только** по ключам. Поэтому если его не пускает, нужно проверять содержимое сгенеренного `.ssh/authorized_keys` и просить пользователя показать вывод `ssh -v` и `id_rsa.pub`.
Если не [добавить ключи в pubkeys CVS](#cvs), то автоматика их затрёт при запуске крона.


## Добавляем пользователя в lusettings.php
Основная конфигурация localuser-db которая растаскивает пользователя с Racktables лежит в файле [lusettings.php](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/blob/master/scripts/localuser-db/lusettings.php)

Править файл можно прямо из UI gitlaba.

Пользователя следует добавить в группу к которой принадлежат его коллеги, либо дефолтный вариант - группа `новичок`.

## Добавляем ключи пользователя в pubkeys {#cvs}
В CVS по *историческим причинам* лежит файл `pubkeys` который является источником правды для ssh-ключей раскатываемых localuser-db.

Формат файла
```
...
<username1>;<ssh-key1>
<username2>;<ssh-key2>
...
```

Чтобы стянуть cvs если у вас его нет нужно сделать так.
Транспорт нашего cvs - это ssh, соответственно у вас должна быть дырка на 22 порт до сервиса cvs.yandex-team.ru
```
# export CVS_RSH=ssh # опционально, явно задать транспорт ssh
cvs -d ":ext:${USER}@tree.yandex.ru:/opt/CVSROOT" co -d conffiles noc/routers/conffiles
cd noc/routers/conffiles
```

Потом добавляем ключи из пользовательского `.ssh/authorized_keys` **СОБЛЮДАЯ ФОРМАТ** `<username>;<ssh-key>` и коммитим.
```
cvs commit pubkeys
```

## Форсим выкатку на слейв
После того как все ручные действия на мастере выполнены имеет смысл выкатить пользователя на слейв. Вообще это происходит по кронджобе `localuser-db.php`. Но это поможет избежать всяких курьезов, типа совпадения по времени выкатки пользователя и переезда мастера. Тем более сделать это очень просто, на мастере просто выполняем:

`php /usr/local/rt-yandex.git/scripts/localuser-db/localuser-db.php -l<username> <slave>`

где,

`<username> - логин нового пользователя`
`<slave>` - имя слейва, те `noc-sas/noc-myt`

Пример запуска
```
[azryve@noc-myt ~]$ php /usr/local/rt-yandex.git/scripts/localuser-db/localuser-db.php -lazryve noc-jump
noc-jump: <0>: retrieving running configuration
noc-jump: <1>: creating user azryve
noc-jump: <1>: updating shell for azryve: /usr/local/bin/bash
noc-jump: <0>: sending commands:
	cat <<\END | sudo cvsworkdir/routers/scripts/userdb-gw.sh cite
	create azryve '4037' 'staff'
	setpass azryve '$1$fKxw8bTG$ALVHqhFn4Uy5qmJxtLB/N/'
	setcomment azryve 'Fedor Zhukov'
	setgroups azryve 'wheel'
	setkeys azryve 'ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDM83vSH04bOdrbHRWZwzZ/7c9+/1nJcq5XrCDeHu5o2snjzGJBCp+qgQetEBHiY3EnkCgBLOwMC4PK5yncKRh1Uwl6B7ElyKd1kOZwXf3lt5EN30M3IjdN9jkRzPlEHzwgws2+x3+7M78rsGmrRHy244yM7yqSbCKf2UcEXTqMXlsMQPATEMB0RqCEwmC923cpfgpHtjKScdHUTMjb3c0apX9MyOxodizi8+1zZeecSpD/LOZIC3IZdpac5Rj/1NoGiGfZHCvs4vKIN0r0xfoIEwmZNJriyA0E2Cv0G43WEzV9lh2zo8vwrg3yRKUk8N9bQrPGcZ9mlMjiZmTNNVmP azryve@azryve-osx'
	chsh azryve /usr/local/bin/bash
	END
noc-jump: <0>: pushing commands to the device
```

Если скрипт не дает желаемого сплева, стоит убедиться что:

* пользователь уже не доехал до слейва самостоятельно
* пользователь добавлен в `lusettings`

## Создаем учетку в Racktables и ставим теги пользователю
После добавления пользователя следует добавить локальную учетку в Racktables.

Тогда на него можно будет ставить произвольные пользовательские теги которые проинтегрированы с permissions и localuserdb.

* Заходим в [RT -> Configuration -> Local users -> Edit](https://racktables.yandex-team.ru/index.php?page=userlist&tab=edit)
* Вставляем в поле **Username** логином нового пользователя, а в **Password** временный пароль из предыдущего шага
* Вешаем на пользователя теги и жмем save

Обычно для нового сотрудника теги ставится `{novice NOC}`. Текущие роли, в порядке возрастания способности ~~ломать сеть~~ наносить добро:

* `{novice NOC}`
* `{intermediate NOC}`
* `{advanced NOC}`
* `{админ RT}`

Подробнее, что может и не может тот или иной обладатель тега нужно смотреть в [RT -> Configuration -> Permissions](https://racktables.yandex-team.ru/index.php?page=perms).
