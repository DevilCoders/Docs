# mobile-realty-bot-android

## Getting started
Чтобы запустить realty-bot-android, нужно выполнить несколько простых шагов:
1. Скачать и установить [Python 3](https://www.python.org/downloads/)
2. Установить pip3. Инструкция [здесь](https://stackoverflow.com/a/6587528)
3. Установить все необходимые зависимости для работы сервера:
   - requirements: `pip3 install -r requirements.txt`
   - startrek-python-client: `pip3 install -i https://pypi.yandex-team.ru/simple/ startrek_client`
   - Vault: `pip3 install yandex-passport-vault-client -i https://pypi.yandex-team.ru/simple`
4. Зайти в директорию, где расположен файл `main.py` и запустить сервер в отдельном процессе: `python3 main.py &`

Также перед запуском следует убедиться, что в файле конфигурации `config.py` глобальная переменная `isDebug` установлена в `false`, в противном случае заработает тестовый бот вместо обычного.
