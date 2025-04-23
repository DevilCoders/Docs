Необходимо:
1) получить ml_engine_app_token <a href="https://oauth.yandex-team.ru/authorize?response_type=token&client_id=37053ffeeb0b4099bafd84242d5850a5"> по ссылке </a>
2) поставить этот токен в ~/.yt/token
3) создать ~/.vhrc файл следующего вида:
```bash
--oauth-token <ml_engine_token>
--yt-token <ml_engine_token>
--yt-token-secret <login>_ml_engine_app_token
--secret=<login>_ml_engine_app_token=<ml_engine_token>
```
`<ml_engine_token>` - токен, полученный в пункте 1
`<login>` - логин на стаффе

Если что-то не работает, писать jruziev@.
