# Выгрузка роутов в бункер
--------------------------

Для выгрузки роутов в бункер необходимо:
  - получить свой OAuth токен [отсюда](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=cf7050262c1d46db8a1637797226df4d)
  - добавить его в переменную окружения BUNKER_API_TOKEN (`export BUNKER_API_TOKEN=<token>` в ~/.bash_profile)
  - запустить 
  ```bash
  npm run bunker:routes:upload
  ```
  - вы великолепны
