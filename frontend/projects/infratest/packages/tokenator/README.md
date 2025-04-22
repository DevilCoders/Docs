# tokenator

Библиотека для работы с токенами FEI. Не является универсальной и конфигурируемой.

## Принудительное переполучение токена
```bash
./bin/tokenator -t sandbox -f
```
Несколько токенов указываются через запятую:
```bash
./bin/tokenator -t sandbox,startrek -f
```
Можно смотреть debug-вывод:
```bash
DEBUG='si:tokenator' ./bin/tokenator -t sandbox,startrek -f
```

## Автоматическое получение токенов
Для получения токенов используются fei-cli:
* для внутреннего OAuth – [link](https://oauth.yandex-team.ru/client/fa9c805e4b9b4c118d4f4e10b4ed0456)
* для внутреннего Github – [link](https://github.yandex-team.ru/settings/connections/applications/63a8ddec02844383c343)

Для получения грантов нового приложения нужно изменить их, авторизовавшись под `robot-serp-bot`

## Пример использования
```js
const tokenator = require('@yandex-int/tokenator');

const tokens = await tokenator(['sandbox', 'startrek']);
const sandboxToken = tokens.sandbox;
const startrekToken = tokens.startrek;
```
