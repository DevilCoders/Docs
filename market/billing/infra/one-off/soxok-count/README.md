# Скрипт для подсчета SOXOK'ов за период

Скрипт принимает в себя 2 аргумента:

1) OAuth-токен как первый аргумент, либо как занчение ENV "ST_OAUTH_TOKEN"
2) Дату начала отсчета как второй аргумент, либо первый если токен в ENV

Примеры использования:

```bash
python3 SoxokCount.py some_token 2022-06-01
ST_OAUTH_TOKEN=some_token python3 SoxokCount.py 2022-06-01
```

Для использования необходим модуль "requests".
Установить его можно с помощью

```bash
pip3 install -U requests 
```
