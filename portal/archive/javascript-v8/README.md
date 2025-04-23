# perl-javascript-v8
Форк https://github.com/dgl/javascript-v8/ с фиксами на утечку памяти + тесты @4eb0da отсюда https://github.com/4eb0da/javascript-v8/

## Зависимости

* v8 JavaScript engine
* perl
* ExtUtils::XSpp

Для тестов:

* Test::Number::Delta

### В пакетах для африканских линуксов

* libv8-3.15
* libv8-dev
* libtest-number-delta-perl
* libextutils-xspp-perl
* gcc

Установить одной командой:
`make deb-build-deps`

## Сборка

`make`

### Сборка deb пакета

Есть специальная цель `deb` которая билдит deb-пакет и все с ним связанное в папочку `deb`. По умолчанию будет пытаться подписать пакет, поэтому необходимо выполнить:
```
eval "$(gpg-agent --daemon)"
export DEBSIGN_KEYID="gragory@yandex-team.ru"
export DEBEMAIL="gragory@yandex-team.ru"
export DEBFULLNAME="Grigoriy Koudrenko"
make deb
```

Если нужно передать альтернативные аргументы debuild, то сделать это можно через переменную `DEBUILD_ARGS`, например собрать пакет без подписи:
```
make deb DEBUILD_ARGS="-uc -us"
```

### dupload

```
cd deb
dupload libjavascript-v8-perl-portal_VERSION_ARCH.changes
```

## Тесты

`make test`

## Установка

`make install`

### Лкально в дев

`make install-dev INSTANCE=v13d0`


