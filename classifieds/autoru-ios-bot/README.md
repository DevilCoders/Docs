# autoru-ios-bot

## Локальная разработка
1. Установить зависимости:
```bash
pip3 install -i https://pypi.yandex-team.ru/simple/ startrek_client
pip3 install -r requirements.txt
```
2. Положить в корень файл `.env`:
```
DEBUG=1
TEAMCITY_TOKEN=...
STARTREK_TOKEN=...
_DEPLOY_METRICS_PORT=8081
```
3. Запустить бота: 
```
export $(cat .env | xargs) && python3 main.py
```


## Сборка для деплоя
Чтобы собрать и выложить изменения:
1. Авторизоваться в registry.yandex.net: 
```
docker login -u <staff login> -p <oauth token> registry.yandex.net
```
2. Выполнить в `utils/`: 
```
./build_and_push_docker_image.sh <new version>
```

Список версий можно узнать так: 
```
curl -H "Authorization: OAuth <token>" -v https://registry.yandex.net/v2/vertis/autoru-ios-bot/tags/list
```

Дальше можно деплоить новую версию, например через бота https://t.me/vertis_shiva_bot:
`/run -l prod -v <version> autoru-ios-bot`

Если нужно прокинуть через переменные окружения новые секреты, то дополнительно нужно исправить [манифест деплоя](https://a.yandex-team.ru/arcadia/classifieds/services/deploy/autoru-ios-bot.yml) и [делегировать секреты](https://docs.yandex-team.ru/classifieds-infra/deploy/secret).
