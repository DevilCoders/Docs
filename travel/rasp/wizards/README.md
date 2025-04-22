# Train-wizard-api
API для колдунчика поездов

# Ручки
[Документация](./train_wizard_api/views/README.md)

# Teamcity
[Собрать контейнер и выкатить в тестинг](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Rasp_TrainWizardApi_BuildAndRelaseToTesting) \
[Расскатить контейнер по проду](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Rasp_TrainWizardApi_RelaseToProduction)

# Qloud
[Проект](https://qloud-ext.yandex-team.ru/projects/rasp/train-wizard-api/)\
[Тестинг](https://qloud-ext.yandex-team.ru/projects/rasp/train-wizard-api/testing)\
[Продакшн](https://qloud-ext.yandex-team.ru/projects/rasp/train-wizard-api/production)

# TestEnv
[Сборка и выкатка образов](https://beta-testenv.yandex-team.ru/projects?name=rasp_wizard_proxy_api)

# Как начать разработку?

1. Готовим настройки и зависимости:
```bash
ya make travel/rasp/wizards
cd travel/rasp/wizards
cp ./tools/samples/local_settings.example.py <project_name>/bin/app/local_settings.py
```
Правим в local_settings.py строчку с <project_name>
```bash
cp ./tools/samples/env_example travel/rasp/wizards/.env
../library/common/virtualenv-setup.py
```

2. Подставляем в local_settings актуальные `DBAAS_OAUTH_TOKEN` и `DBAAS_TRAIN_WIZARD_API_DB_PASSWORD` (берём в секретнице).

3. Если разрабатываемся на виртуалке, которой нет в кондукторе, то прописываем в local_settings её ДЦ: `YANDEX_DATA_CENTER = 'sas'`
Чтобы не ходит в кондуктор, нужна переменная (она есть в env-example):
```bash
export YANDEX_ENVIRONMENT_TYPE=testing
```

4. Собрать бинарник
Флаг RASP_DEV включает использование local_settings
```bash
cd <project_name>
ya make -D=RASP_DEV
```

5. Собрать докер-образ
```bash
ya package ./pkg.json --docker --docker-repository rasp
```

6. Запустить докер-образ локально:
```bash
docker run --env-file .env -p 127.0.0.1:<port>:80 <image_id>
```

7. Собранный докер-образ можно пушить как есть, он попадет в правильный репозиторий и будет виден в qloud
```bash
docker push <image_path>
```


# Как работать с переводами

## Добавить новый язык
```bash
newlang=eo
../library/common/virtualenv/bin/pybabel init --domain=django --input-file=wizard_lib/locale/django.pot --output-dir=wizard_lib/locale/ --locale ${newlang}
```

## Отправить новые ключи для перевода в танкер

1. Получаем токен для работы с танкером на странице https://nda.ya.ru/3SjQY7 .
2. Стоит проверить права на проект rasp в Танкере: https://doc.yandex-team.ru/Tanker/general-info/concepts/access.html .
3. Пишем в `local_settings.py`:
```python
TANKER_TOKEN = 'OAuth <ваш токен>'
```
4. Собираем новые ключи
(для этого может потребоваться настроить virtualenv и установить пакет Babel через pip,
в Аркадии есть Babel, но только в виде библиотеки):
```bash
cd travel/rasp/wizards
../library/common/virtualenv/bin/pybabel extract --omit-header --sort-by-file --mapping-file=babel.cfg --output-file=wizard_lib/locale/django.pot \
    proxy_api/ suburban_wizard_api/ train_wizard_api/ wizard_lib/
../library/common/virtualenv/bin/pybabel update --no-fuzzy-matching --no-wrap --domain=django --input-file=wizard_lib/locale/django.pot --output-dir=wizard_lib/locale
```
5. Отправляем их в танкер:
```bash
DJANGO_SETTINGS_MODULE=local_settings Y_PYTHON_ENTRY_POINT=travel.rasp.wizards.<project_name>.app:manage bin/app/app tankerupload django:wizardia
```
В том случае, если не заработает отправка ключей в Танкер, их можно добавить вручную тут:
https://tanker.yandex-team.ru/?project=rasp&branch=master&keyset=wizardia

## Получить переводы из танкера
```bash
cd travel/rasp/wizards/<project_name>
DJANGO_SETTINGS_MODULE=local_settings Y_PYTHON_ENTRY_POINT=travel.rasp.wizards.<project_name>.app:manage bin/app/app tankerdownload django:wizardia
../library/common/virtualenv/bin/pybabel compile --domain=django --directory=../wizard_lib/locale --statistics
```

# Как работать с protobuf
## Собираем protoc(компилятор protobuf схем)
1. Идем сюда https://developers.google.com/protocol-buffers/docs/pythontutorial
2. <CTRL + F> Compiling Your Protocol Buffers
3. Идем по инструкции и собираем свеженький компилятор

## Как перекомпилировать protobuf схемы
1. Идем в корень репозитория
2. ```protoc -I ./wizard_lib/protobuf_models/ --python_out ./wizard_lib/protobuf_models/ ./wizard_lib/protobuf_models/*.proto```

# Как запускать тесты
Для каждого субрепозитория из proxy_api, train_wizard_api, suburban_wizard_api
Переходим в директорию субрепозитория.
```bash
ya make -tt
```
