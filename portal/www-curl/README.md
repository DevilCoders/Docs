# WWW-Curl
Кастомные биндинги для WWW::Curl от морды

# Как собирать
```
  sudo apt-get update
  sudo apt-get install libcurl4-openssl-dev libtest-cpan-meta-perl\
    libtest-pod-coverage-perl libtest-pod-perl devscripts build-essential
  (
      set -x
      set -e
      cd libwww-curl-perl
      eval "$(gpg-agent --daemon)"
      export DEBSIGN_KEYID="gragory@yandex-team.ru"
      export DEBEMAIL="gragory@yandex-team.ru"
      export DEBFULLNAME="Grigoriy Koudrenko"
      dch -i
      debuild -b
  )
```

# Загрузить на dupload

Натсроить dupload и выполнить команду

```
dupload --to morda-xenial libwww-curl-perl_VERSION_ARCH.changes
```
