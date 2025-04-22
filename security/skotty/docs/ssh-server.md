# Настройка SSH: кастомный сервер

{% note warning %}

Раздел находится в разработке. Если у вас кастомный SSH-сервер, пожалуйста, прийдите в security@yandex-team.ru, мы обсудим варианты и дадим рекомендации.

{% endnote %}

На серверной стороне нам нужно настроить две вещи - доверие к SSH CA и аутентификация в sudo:
  1. Устанавливаем пакет `yandex-skotty-pam`

  2. Настраиваем PAM для sudo (добавляем аутентификацию с помощью [pam_skotty_sudo.so](https://a.yandex-team.ru/arc/trunk/arcadia/security/skotty/pam_skotty_sudo)):
```
# /etc/pam.d/sudo
#%PAM-1.0

session    required   pam_env.so readenv=1 user_readenv=0
session    required   pam_env.so readenv=1 envfile=/etc/default/locale user_readenv=0

# success=<N> нужно будет тюнить
auth [success=3 default=ignore] /lib/security/pam_skotty_sudo.so
@include common-auth
@include common-account
@include common-session-noninteractive
```

  3. Затем конфигурим SSHD:
```
# /etc/ssh/ssh_ca - CA, которым SSH будет безоговорочно верить. В нашем случае - только секурные ключики
ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBJnF1UG50PejZLaFFAWTMOL7e4xy44Z/mDJyF6RTsQsIxFN2oC9E4cwOTKSf2Ko/jemdnDOWu+j8X6f4y2KTV5M= # secure

# /etc/ssh/trusted_sudo_ca - доверенный CA для sudo
ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBGu6MjOjHX9R4w/1EZ+0A938E5O63iTAc3HAM6ixrX0wx5XuS8WFm+xxZotYloqtS2LnZ1lWe6IHPh5jVIplCaY= # sudo

# /etc/ssh/sshd_config
TrustedUserCAKeys /etc/ssh/ssh_ca
AuthorizedPrincipalsFile /etc/ssh/principals/%u # хранит альтернативных принципалов, иначе SSH разрешит вход только принципалу из сертификата
AuthorizedKeysFile /etc/ssh/users/%u # пользовательские ключики, чтоб не шарахаться по домашкам + пользователи не могли сами рулить ключами
RevokedKeys /etc/ssh/revoked_keys # путь к KRL

# /etc/ssh/principals/root - список пользователей, кому разрешен вход рутом, например, разрешает входить рутом сервер-админам:
buglloc
ezaitov

# /etc/ssh/users/buglloc - альтернативно разрешаем юзеру:
#  * вход не только секурными ключиками, но и обычными
#  * легаси ключами со стаффа
cert-authority ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBP8w+sr7XJuSXHQ9OAOj0eRfv4fQi/qFnW185Ae5fkKX9VhtmkM7LpfIy7NeOOthxS9wUJmfEcAGUrSH5Pry/ZU= # insecure
# old RSA keys below...
```

Далее предполагается, что условный cauth-agent:
  - заимеет настройку того с какими ключами пользователей пускать их на хост (т.е. насколько секурен должен быть ключ), на текущий момент у нас есть три варианта:
    * только `secure` ключи - обновляем с мастера только `/etc/ssh/ssh_ca`
    * плюс `insecure` ключи - обновляем authorized keys пользователей (`/etc/ssh/users/%u`), добавив для каждого пользователя соотв. `cert-authority`
    * плюс `legacy` - обновляем authorized keys пользователей (`/etc/ssh/users/%u`), добавив для каждого пользователя его authorized keys со стаффа
  - вместе с обновлением [serveradmins](https://cauth.yandex.net:4443/passwd/serveradmins/) будет прописывать этих пользователей в `/etc/ssh/principals/root`
  - синкать `/etc/ssh/trusted_sudo_ca`
  - синкать `/etc/ssh/revoked_keys`

Почему все именно так:
  - синкаем публичные ключи CA на случай ЧП
  - уносим authorized keys из хомяков, чтоб 1) не шарахаться по ним, это довольно багоопасно (и такие случаи у cauth были) 2) запретить пользователям самим крутить их
  - CA расположены от более безопасного к менее:
    * дефолтный у нас `secure`, чтоб войти рутом можно было только с безопасным ключиком
    * а дальше уже для каждого пользователя ослабляем

Такая конфигурация должна позволить как плавно мигрировать на безопасное хранение ключей и passwordless sudo, так и контролировать необходимую степень секурности. Т.е.:
  - первым этапом мы просто добавляем возможность входить новыми ключиками и аутентифицироваться в sudo с помощью ключа => ничего никому не ломаем
  - вторым (когда у всех есть юбики):
    * отключаем `pam_unix.so` и `pam_sss.so` => делать парольное sudo можно будет только с ключиком
    * отключаем в `cauth-agent` принос `legacy` ключей со стаффа

## Координаты ручек для забора всех нужных данных

  - `https://cauth.yandex.net:4443/keylists/main/secure` - публичные ключи Secure CA
  - `https://cauth.yandex.net:4443/keylists/main/insecure` - публичные ключи Insecure CA
  - `https://cauth.yandex.net:4443/keylists/main/sudo` - публичные ключи Sudo CA
  - `https://cauth.yandex.net:4443/keylists/main/all.zst` - KRL

Подробнее о ротации ключах CA можно почитать в [How it works: CA keys](https://docs.yandex-team.ru/skotty/how-it-works-ca-keys), а о KRL в [How it works: KRL](https://docs.yandex-team.ru/skotty/how-it-works-krl).
