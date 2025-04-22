## Установка и запуск
```sh
git clone git@github.yandex-team.ru:mm-interfaces/sinsig-mobile-viewer.git
cd ./sinsig-mobile-viewer
npm i
npm start
open https://localhost:9001
```

## Деплой шаблона
В директории проекта создайте файл `yang.secret.json` со следующим содержимым:
```json
{
  "prod": "<prod-oauth-token>",
  "sandbox": "<sandbox-oauth-token>",
}
```
* Токен [prod-oauth-token](https://yav.yandex-team.ru/edit/secret/sec-01d2w5sp6m2kmcj90spk7q2ksn/explore/versions)
* Токен [sandbox-oauth-token](https://yav.yandex-team.ru/edit/secret/sec-01d2w5x3frsfvtxq6z2yd5acb5/explore/versions)

После этого необходимо выполнить одну из следующих команд:
```sh
npm run deploy:sandbox
npm run deploy:prod
npm run deploy:batch
```
