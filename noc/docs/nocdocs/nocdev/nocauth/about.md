# Nocauth

Nocauth - это инструмент, который позволяет заходить на сетевые устройства по SSH, при этом доступы настраиваются через IDM, а не на каждом устройстве по отдельности.

## Какие проблемы решаются

* Для новых сотрудников нужно проделывать кучу работы по добавлению их на устройства. И наоборот - для увольняющихся.
* На некоторых устройствах есть ограничение на количество ключей, поэтому туда нельзя добавить больше пользователей.
* Некоторые устройства не поддерживают аутентификацию по ключу.

## Как пользоваться

Доступы на устройства хранятся в IDM, система [Nocauth](https://idm.yandex-team.ru/system/nocauth/roles).

Чтобы ходить на устройства, проще всего использовать наши обёртки над `ssh` и `scp`: `nocssh` и `nocscp` соответственно.

Пишете:
```
> nocssh <имя устройства>
```
и попадаете на устройство (если у вас есть ключ на стафе и доступ в IDM). Все аргументы `ssh` и `scp` поддерживаются. Если вы идёте куда-то, где ещё не настроен Nocauth, произойдёт фолбек на обычные `ssh` / `scp`

## Установка на Ubuntu

```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7FCD11186050CD1A
sudo add-apt-repository "deb http://common.dist.yandex.ru/common stable/all/"
sudo apt-get update
sudo apt-get install yandex-nocauth
```

## Установка на MacOS

```
brew tap nocdev/tap https://noc-gitlab.yandex-team.ru/nocdev/nocauth.git
brew install nocauth
```

## Установка на FreeBSD

Пакетов и портов пока нет, но `nocssh` и `nocscp` уже установлены на `noc-sas` и `noc-myt`.

## Хождение на устройство напрямую

Можно ходить на устройство напрямую, но в таком случае аутентификация только по паролю, а не по ключам. Нужно указать пользователя с суффиксом `-nocauth`, например, `LOGIN-nocauth`. Нужно будет ввести либо свой доменный пароль, либо пароль, который у вас был на устройстве раньше (Nocauth хранит базу существующих хешей). Минус такого подхода - Nocauth пока раскатан не везде, так что доменный пароль может не сработать.

## Автор статьи

Влад Старостин - vladstar@yandex-team.ru
