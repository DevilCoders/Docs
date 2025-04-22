[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/logistics/lms/lms-frontend&vcs=arc)](https://oko.yandex-team.ru/arc/market/logistics/lms/lms-frontend)

## Админка LMS

### Node

Для сборки используется node версии 11.7.0, для установки лучше настроить себе **node version manager**

`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash` для bash

`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | zsh` для zsh

#### Установка и конфигурация

На версии 11.7.0 не соберется, можно использовать последнюю

`nvm install 14.4.0`

`nvm use 14.4.0`

Подробнее ознакомиться с nvm можно [тут](https://github.com/nvm-sh/nvm)

### Yarn

Для сборки используется yarn версии 1.14.0, для установки лучше
настроить себе **yarn version manager**

`brew install tophat/bar/yvm`

или

`curl -s https://raw.githubusercontent.com/tophat/yvm/master/scripts/install.js | node`

#### Установка и конфигурация

Аналогичная история, локально собирается последней версией

`yvm install 1.22.4`

`yvm use 1.22.4`

Подробнее ознакомиться с yvm можно [тут](https://yvm.js.org/docs/overview)

### Локальная сборка и запуск Yarn

После конфигурации node и yarn локально проект собирается при помощи
`yarn install`

При этом по файлу **package.json** будет сгенерирована папка **node_modules** с зависимостями, а также файл **yarn.lock**

После сборки желательно убедиться, что в Intellij IDEA Preferences->Languages&Frameworks->Node.js and NPM/TypeScript выбраны правильные версии и теперь можно использовать встроенный в Intellij IDEA плагин TypeScript для компиляции и проверки на ошибки

Запускается при помощи `yarn start`

### Локальная сборка и запуск ya.make

Для аркадийной сборки используется скрипт /build-tools/build.py **которому нужны три архива: для node, yarn и node_modules**

В файлах node.ya.make/yarn.ya.make/node_modules.ya.make указаны идентификаторы соответствующих ресурсов в sandbox для архивов

При добавлении новых зависимостей в **package.json** необходимо после сборки yarn обновить ресурс в node_modules.ya.make

#### Архивация

`tar czf node_modules.tar.gz node_modules`

#### Загрузка в sandbox

`ya upload --ttl=inf -T=JAVA_LIBRARY -d="Logistics Management Service Admin node_modules" node_modules.tar.gz`

После этого меняется идентификатор в **node_modules.ya.make**

### Обновление версии Node/Yarn

При обновлении версии node или yarn необходимо аналогичным образом
обновить ресурсы node.tar.gz/yarn.tar.gz

Текущее расположение для архивации можно узнать вот так
`nvm which current` или `yvm which current`

#### Пример для Yarn

yarn which current выдал /usr/local/Cellar/yvm/3.6.7/versions/v1.22.4/bin/yarn

Все содержимое папки v1.22.4 копируется в отдельную папку node и архивируется

`mkdir yarn`

`cp -R /usr/local/Cellar/yvm/3.6.7/versions/v1.22.4/yarn`

`tar czf yarn.tar.gz yarn`

Аналогично node_modules аплоудится с указанием версии в описании
и меняется идентификатор ресурса в sandbox в **yarn.ya.make**

`ya upload --ttl=inf -T=JAVA_LIBRARY -d="v1.22.4" yarn.tar.gz`

#### Пример для Node

Так как необходимо два разных бинарника OS_LINUX и OS_DARWIN, то удобнее
всего скачать архивы прямо с официального сайта и их уже аплоудить в sandbox, не забыв поменять идентификаторы ресурсов в **node.ya.make**

Например, для текущей версии 14.4.0 https://nodejs.org/dist/v14.4.0/

Это будут архивы

**node-v14.4.0-linux-x64.tar.gz** OS_LINUX

**node-v14.4.0-darwin-x64.tar.gz** OS_DARWIN

Надо их переупаковать перед аплоудом в sandbox, переименовав папку **node-v14.4.0-linux-x64 в папку node** и также для 2 архива

### Публикация изменений

1. Добавить зависимости с помощью `yarn add`.
1. Локально собрать при помощи `ya make`.
1. Архивировать директорию node_modules: `tar czf node_modules.tar.gz node_modules`.
1. Опубликовать изменения в сандбокс:
   `ya upload -T=JAVA_LIBRARY -d="Logistics Management Service Admin node_modules" --ttl=inf node_modules.tar.gz`

    Подробнее ознакомиться с сандбоксом можно [тут](https://wiki.yandex-team.ru/sandbox)

1. После публикации будет выведена информация о ресурсе. Примерно так:

    ```
    Created resource id is 123456789
                TTL          : INF
                Resource link: https://sandbox.yandex-team.ru/resource/123456789/view
                Download link: https://proxy.sandbox.yandex-team.ru/123456789
    ```

    Идентификатор ресурса указан после **Created resource id is**.
    Чтобы посмотреть информацию о ресурсе, можно перейти по ссылке **Resource link**.
    Скачать ресурс можно по ссылке **Download link**.

1. Нужно скопировать идентификатор ресурса в файл **node_modules.ya.make**, заменив старый идентификатор после
   ключевого слова **FILE**.
1. Если архивировали в той же папке, что и **node_modules**, нужно удалить **node_modules.tar.gz**.
   **package-lock.json** и **yarn-error.log** коммитить и пушить не надо.
1. Как только ресурс будет готов (статус **READY**), можно проверить зависимости с помощью `npm install`.

**_ВАЖНО_**: Не забыть обновить **node_modules.ya.make** свежей версией ресурса если это необходимо!
А также **node.ya.make/yarn.ya.make** если потребовалось обновление их версий!

### Генерация типов и api (Hrms)

* Генерация запускается по команде ``yarn generate:api``
* Сейчас на бекенде нет общего правила для именования проскированных роутов,
 поэтому при добавлении нового роута в директории ``api-generaton/index.js`` надо добавить маппинг для
 нового роута вручную
