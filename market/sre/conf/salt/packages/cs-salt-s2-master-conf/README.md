# yandex-market-salt-master-conf

Конфиги для salt master Маркета

## Использование
* Основные параметры мастера пишутся в `src/market.conf` - пакет поместит его `/etc/salt/master.d/market.conf`
* Если вы считаете необходимым, можете размещать свои параметры в отдельных файлах с расширением `.conf` внутри директории `src/`

## GPG
Для функциональности деплоя секретных файлов и сертификатов, конфигурация мастера включает набор GPG-ключей. Ключи расположены в yav секрете https://yav.yandex-team.ru/secret/sec-01fz6dgr3pzam15xvtjnqte8c1/explore/versions.
#### Установка новых ключей на сервер с мастером:
* При наличии yav токена на мастер сервере ключи заипортируются при установке пакета, если этого не произошло, то нужно их заимпортировать вручную:
```shell
YAV_TOKEN=$(cat /etc/datasources/yav-token) yav get version sec-01fz6dgr3pzam15xvtjnqte8c1 -O public | gpg --homedir /etc/salt/gpgkeys --import
YAV_TOKEN=$(cat /etc/datasources/yav-token) yav get version sec-01fz6dgr3pzam15xvtjnqte8c1 -O private | gpg --homedir /etc/salt/gpgkeys --import
```
