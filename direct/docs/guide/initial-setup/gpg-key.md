# Создание GPG-ключа и загрузка его на staff

{% note info %}

Все действия выполняем на [ppcdev](../../glossary/glossary.md#ppcdev)

{% endnote %}

## Создание GPG-ключа { #create-key }

### Запускаем создание
Из консоли выполняем команду:
```sh
gpg --gen-key
```
Она выведет:
```text
gpg (GnuPG) 1.4.16; Copyright (C) 2013 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
Your selection?
```
### Тип ключа { #key-type }
Нам нужен **DSA and Elgamal**, поэтому вводим **2** и нажимаем `<ENTER>`.  
Покажут допустимые размеры ключа для выбранного типа:
```text
DSA keys may be between 1024 and 3072 bits long.
What keysize do you want?
```

### Размер ключа { #key-size }
Выбираем по вкусу: **2048** или **3072**, вводим это число и нажимаем `<ENTER>`.  
Выведет выбранное значение:
```text
Requested keysize is 3072 bits
```

### Срок действия ключа { #key-lifetime }
После выбора размера, нас попросят указать срок действия ключа:
```text
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0)
```
Соглашаемся с предложенным вариантом (0 — бессрочно). Просто нажимаем `<ENTER>`.

{% note tip %}

Для параноиков — указать срок жизни ключа можно, например полгода.  
Основая проблема с этим — ключ всегда протухает в самый неподходящий момент.

{% endnote %}

Нас переспросят:
```text
Key does not expire at all
Is this correct? (y/N)
```
Соглашаемся: вводим **y** и нажимаем `<ENTER>`.

### User ID
Попросят представиться:
```text
You need a user ID to identify your key; the software constructs the user ID
from the Real Name, Comment and Email Address in this form:
    "Heinrich Heine (Der Dichter) <heinrichh@duesseldorf.de>"

Real name:
```
Вводим своё имя латиницей, например **Alexandr Duplishchev** и нажимаем `<ENTER>`.

Спросят почту:
```text
Email address:
```
Вводим свою рабочую почту, например: **ppalex@yandex-team.ru** и нажимам `<ENTER>`.

Спросят комментарий к ключу:
```text
Comment:
```
Ничего не вводим, нажимаем `<ENTER>`.

Нам покажут что получилось и попросят подтверждение:
```text
You selected this USER-ID:
    "Alexandr Duplishchev <ppalex@yandex-team.ru>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit?
```
Если все хорошо, вводим **O** (латинская буква) и нажимаем `<ENTER>`.

### Пароль от ключа
Предложат ввести пароль от ключа:
```text
You need a Passphrase to protect your secret key.

Enter passphrase:
```
Придумываем пароль, **хорошенько запоминаем**.  
Вводим, нажимаем `<ENTER>`.

Попросят повторить ввод:
```text
Repeat passphrase:
```
Вводим ещё раз придуманный пароль, нажимаем `<ENTER>`.

### Генерация ключа
Утилита выведет что-то вроде этого:
```text
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: WARNING: some OpenPGP programs can't handle a DSA key with this digest size
++++++++++++++++++++...+++++.++++++++++++++++++++++++++++++.+++++++++++++++...++++++++++.+++++++++++++++.....+++++...+++++......+++++++++++++++.++++++++++.....+++++..++++++++++++++++++++>++++++++++.++++++++++++++++++++.+++++.++++++++++>+++++>+++++.>+++++....+++++
```
Нужно будет немного подождать.

### Готово
Нам покажут информацию о созданном ключе:
```text
gpg: key 93254B10 marked as ultimately trusted
public and secret key created and signed.

gpg: checking the trustdb
gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model
gpg: depth: 0  valid:  11  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 11u
gpg: next trustdb check due at 2021-04-07
pub   3072D/93254B10 2020-10-07 [expires: 2021-04-07]
      Key fingerprint = BB60 FED2 13F5 C531 E825  BD6E 3B32 21DB 9325 4B10
uid                  Alexandr Duplishchev <ppalex@yandex-team.ru>
sub   3072g/6F4DF63C 2020-10-07 [expires: 2021-04-07]
```
Обратите внимание, здесь в первой строке: **93254B10** — это ID ключа, он нам понадобится.


## Загрузка ключа на staff { #upload-to-staff }
### Получение ключа { #get-key }
Выполняем в консоли:

{% list tabs %}

- простой вариант

   _подходит, если созданный только что ключ — единственный и других нет_
    ```sh
   gpg --export --armor `whoami`@yandex-team.ru
   ```

- сложный вариант

   _подходит, если GPG-ключей несколько или загрузка на Staff выдает ошибку "Неверный GPG-ключ"_
   ```sh
   gpg --export --armor <ID из предыдущего шага>
   ```

{% endlist %}

Нам распечатают ключ:
```text
-----BEGIN PGP PUBLIC KEY BLOCK-----
Version: GnuPG v1

mQSuBF99roQRDAD6conwgqgqPI8WmbnXlBLaAamxE9ic/NxdedjMdD3+lTUmJjBL
..... <тут будет много похожих строк> .....
dOl5g+IRIE7XeUm60b+axznGVC9+rZq1AQCMhjI+HBnmeefW5Mv8DdfIVlLbGfGw
gNjMC89RmeU20w==
=B40i
-----END PGP PUBLIC KEY BLOCK-----
```

### Загрузка на staff { #upload-key }
Открываем свою страницу [staff.yandex-team.ru](https://staff.yandex-team.ru).

Наводим курсор на раздел **GPG-ключи** — появится иконка карандаша.
Нажимаем на неё — откроется попап редактирования GPG-ключей.  
В нём нажимаем **Добавить ключ**:
- в поле **Ключ** вставляем целиком весь вывод команды `gpg --export --armor ...`

   {% note warning %}

   Вставлять нужно целиком, **включая** строки:  
   `-----BEGIN PGP PUBLIC KEY BLOCK-----` и `-----END PGP PUBLIC KEY BLOCK-----`.

   {% endnote %}

- в поле **Описание** пишем что-нибудь.

Нажимаем **Сохранить**.

{% cut "Поясняющие скриншоты" %}

Редактирование GPG-ключей:
![no alt](_assets/staff-edit-gpg-icon.png "скриншот стаффа")

Добавление ключа:
![no alt](_assets/edit-gpg-popup.png "добавление GPG-ключа")

{% endcut %}

<br/>

### Подождать { #wait }
Нужно выждать час—два, пока ключ разъедется куда нужно.


## Настройка { #setup }

### Настройка окружения { #setup-env }
Добавь в файл `~/.bashrc` строки:
```sh
export DEBFULLNAME="<своё имя латиницей как указал в user ID>"
export DEBEMAIL="<свой login>@yandex-team.ru"
alias dch='dch --distributor=debian'
```
Имя и email нужно указать **в точности также**, как при создании ключа.

{% note info "Если ключ создан с непустым Comment" %}

Его (комментарий) нужно указывать в DEBFULLNAME: `<своё имя латиницей> (<свой комментарий>)`

{% endnote %}

Примеры:

{% list tabs %}

- без комментария
   ```sh
   export DEBFULLNAME="Alexandr Duplishchev"
   export DEBEMAIL="ppalex@yandex-team.ru"
   alias dch='dch --distributor=debian'
   ```
- с комментарием
   ```sh
   export DEBFULLNAME="Dmitry Pushkin (your_comment)"
   export DEBEMAIL="dspushkin@yandex-team.ru"
   alias dch='dch --distributor=debian'
   ```

{% endlist %}

После этого выполни:
```sh
source ~/.bashrc
```

### Настройка GPG-агента { #setup-agent }

{% note info "Использовать GPG-агент или нет" %}

Если ты app-duty, то настроить gpg-агент — обязательно.  
Тебе понадобится собирать хотфиксы для perl-Директа,
а без агента велики шансы пропустить ввод пароля после сборки пакетов,
и это будет случаться в _самый_ неподходящий момент.

Остальным — как хочешь.  
Плюс: пароль достаточно ввести один раз и действовать он будет до перезагрузки сервера.  
Минус: пароль становится очень легко _забыть_.

{% endnote %}

Для настройки добавь в файл `~/.bashrc`:
```sh
which gpg-agent > /dev/null
if [ "$?" -eq 0 ]; then
   if test -f $HOME/.gpg-agent-info &&    kill -0 `cut -d: -f 2 $HOME/.gpg-agent-info` 2>/dev/null; then
       export GPG_AGENT_INFO=`cat $HOME/.gpg-agent-info`
   elif [ -d ~/.gnupg ]; then
       eval `gpg-agent --daemon --default-cache-ttl 86400 --max-cache-ttl 700000`
       echo $GPG_AGENT_INFO >$HOME/.gpg-agent-info
   fi
   export GPG_TTY=`tty`
fi
```
Затем открой (если нужно — создай) файл `~/.gnupg/gpg.conf` и впиши туда (если там такой ещё нет) строку:
```text
use-agent
```

После этого выполни:
```sh
source ~/.bashrc
```

## Проверка
### Параметры окружения
Выполни:
```sh
echo $DEBFULLNAME
echo $DEBEMAIL
```
Должно вывести строки с твоим именем и адресом почты.  
Если пусто — непорядок, нужно разбираться, исправлять.

### Ключ и GPG-agent
Для проверки выполни:
```sh
echo test | gpg --sign > /dev/null && echo ok || echo fail
```
Может спросить пароль от ключа. Если в конце написало **ok** — всё хорошо.

## Ссылки { #links }
* [Предыдущая версия инструкции](https://wiki.yandex-team.ru/direct/development/howto/packages/podgotovka-old/) на вики
* Документация про GPG, читать необязательно:
   * <https://doc.yandex-team.ru/Debian/deb-pckg-guide/concepts/GPG.xml>
   * <https://doc.yandex-team.ru/Debian/deb-pckg-guide/concepts/Repos.xml>

