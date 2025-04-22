# adv-front [![Build Status](https://drone.yandex-team.ru/api/badges/advertising/adv-front/status.svg)](https://drone.yandex-team.ru/advertising/adv-front)

## Документация доступна на Wiki

https://wiki.yandex-team.ru/mace/adv-www/

-----------

Благодаря платформе [magicdev](https://github.yandex-team.ru/project-stub/magicdev#Что-это-зачем-и-как-этим-пользоваться), проект разрабатывается локально.

Для работы потребуется _Node.js 10_ – устанавливаем его по необходимости:

```bash
brew install nvm
nvm install 10
```

Создаем в корне проекта `.env` файл со следующим содержимым: https://wiki.yandex-team.ru/mace/adv-www/dotenv/

Устанавливаем зависимости

```bash
npm run deps
```


При первом запуске создаем `.tvm.json`

```bash
# Устанавливаем CLI секретницы
pip install yandex-passport-vault-client -i https://pypi.yandex-team.ru/simple

# Добавляем ssh ключи для работы CLI секретницы
ssh-add

# Создаем .tvm.json для локальной разработки
npm run tvm:create-json
```

Далее подтягиваем данные и запускаем проект:

```bash
npm run bunker

# Magicdev запросит ваш пароль, чтобы запустить на 443 порту
npm run dev
```

Проект становится доступен по адресу:
https://localhost.msup.yandex.ru/adv/

#### Локальный запуск на других доменах
Локальная сборка всех языков - тяжелая операция, оперативки не хватает. Чтобы поднять сайт на доменах, отличных от ru,
необходимо в default конфиге в поле `langs` добавить нужный язык.

Для поднятия турецкого сайта дополнительно нужно закомментить
[одну строчку](https://github.yandex-team.ru/advertising/adv-front/blob/dev/server/router/router.js#L55).

Сайт для Китая запускается локально на кастомном домене `localhost.msup.yandex-ad.cn`. Сертификат для этого домена закомичен
в репозиторий. Для того чтобы запускаться на этом домене, нужно добавить в файл /etc/hosts следующее правило:
```
# ADV Сайт для Китая
127.0.0.1   localhost.msup.yandex-ad.cn
```

## Tunneler

Для отладки приложения с других устройств используется [Tunneler](https://wiki.yandex-team.ru/q/devops/tunneler/).

Запустить его можно командой:

```bash
./tunel.sh ekb-tunneler.ldev.yandex-team.ru 443 1
```

Проект становится доступен по адресу:
https://<username>-1-ekb.ldev.yandex.ru/adv/

## Мониторинги

Для настройки мониторингов используется [Monitorado](https://github.yandex-team.ru/toolbox/monitorado).

#### Как изменить конфигурацию

* Получаем токен [тут](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=171fcece39a04fd0a6b8b74950336008) и кладем в переменную окружения, записав в `.env`

    ```bash
    MONITORADO_OAUTH_TOKEN=
    ```

* Вносим необходимые изменения в файл `.monitorado.yml`

* Запускаем команды

    ```bash
    # Смотрим, что изменилось
    npx monitorado diff -v

    # Обновляем конфигурацию
    npx monitorado exec -v
    ```

## Выгрузка данных об агенствах

```bash
npm run bunker
node scripts/agencies.js
```


## Сборка Docker-образа с редиректами

```
# https://platform.yandex-team.ru/projects/commerce/adv-rewrites
npm run rewrites
```

## Выгрузка комментариев из Блогов

Создать файл с настройками по типу [такого](https://github.yandex-team.ru/advertising/adv-front/blob/dev/scripts/commentsSettings.js):
* blog - объект с указанием слага и языка блога
* fromPost - id поста, с которого начинать выгрузку
* postsCountToReadFromBlog - количество постов, которое нужно прочитать за один запрос
* postsCountForWriteToFile - количество постов, которое будет записано в файл за раз
* blogsApiUrl - урл до апи блогов
* getPostUrl - функция, которая принимает на вход идентификатор поста и возвращает ссылку на этот пост
* tvm - объект с настройками TVM

Запуск выгрузки:

```bash
node scripts/commentsMigration.js settings_file_path
```

Будут созданы 3 файла: с постами (posts.json), комментариями (comments.json) и не вошедшими в выгрузку комментариями (skip.json),
которые либо удалены (удаленные комментарии не выгружаем), либо данные в них некорректны (например, uid автора).
