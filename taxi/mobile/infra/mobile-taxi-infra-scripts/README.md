# mac-os-setup-scripts

Скрипты для настройки окружения на mac os билд агентах (возможно часть скриптов переедет в saltstack) 

У токена должны быть доступы к сертификатам
*  https://yav.yandex-team.ru/secret/sec-01d0yw2b5bdcbq12xy9ksdaean/explore/versions
*  https://yav.yandex-team.ru/secret/sec-01f0k35vsqjyjahhzz3qjyxrga/explore/versions
*  https://yav.yandex-team.ru/secret/sec-01ehsg7kw4a9g8h0jvpgbwmb9z/explore/versions
*  https://yav.yandex-team.ru/secret/sec-01epys8rnkq2wsrng4jrzx7j16/explore/versions
*  https://yav.yandex-team.ru/secret/sec-01fcz9abr77pt2tcs4dxd7kr7s/explore/versions

Пример использования setup_admin.sh 
Авториозоваться под админ пользователем, вызвать команду

```
curl -o ./setup_admin.sh http://s3.mdst.yandex.net/macos/setupMacOS/setup_admin.sh && \
chmod u+x setup_admin.sh && \
./setup_admin.sh -y YOUR_TOKEN 
```

Пример использования setup_user.sh
Авториозоваться под билд юзером пользователем, вызвать команду

```
curl -o ./setup_user.sh http://s3.mdst.yandex.net/macos/setupMacOS/setup_user.sh && \
chmod u+x setup_user.sh && \
./setup_user.sh -y YOUR_TOKEN
```
