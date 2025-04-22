# Поисково-макетный шаблон SbS 

# Инициализация и запуск

#### Получение токена
Окружения Толоки:
  - **sandbox** - [sandbox.toloka.yandex.ru](https://sandbox.toloka.yandex.ru/)
  - **prod** - [toloka.yandex.ru](https://toloka.yandex.ru/)

Окружения Янга:
  - **sandbox** - [sandbox.yang.yandex-team.ru](https://sandbox.yang.yandex-team.ru/)
  - **prod** - [yang.yandex-team.ru](https://yang.yandex-team.ru/)
  
[Токены лежат здесь](https://yav.yandex-team.ru/secret/sec-01cn53b0mcf16njk1haxjrzp3n/explore/versions)

Также получить токены можно в личном кабинете, как это сделано описано [на странице документации Яндекс.Толока](https://tech.yandex.ru/toloka/doc/concepts/access-docpage/).

#### Инициализация токенов
В корне (на уровне package.json) необходимо создать файл **samadhi.secret.json** со следующим содержимым:
```json
{
  "sandbox": "Ваш токен для sandbox Толоки",
  "production": "Ваш токен для production Толоки",
  "yang-sbox": "Ваш токен для sandbox Янга",
  "yang-prod": "Ваш токен для production Янга"
}
```
  
#### Запуск проекта
Для запуска необходимо выолнить следующие команды
```sh
npm run search-react:build
npm run search-react:ttk:server
npm i
open https://localhost:9001
open https://localhost:8083/assets/script.js
```
В открывшихся вкладках может потребоваться сделать исключение по безопасности. Сделать это нужно как для дев-сервера вебпака, так и для сервера толоки. основное приложение будет открыто по первой ссылке.

# Деплой шаблона
##### Деплой на конкретный проект:
```sh
npm run search-react:build-release
npm run search-react:deploy -- --mode <TOLOKA_ENV: sandbox | production | yang-sbox> --project <PROJECT_ID>
```
