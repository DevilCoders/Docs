# Личный кабинет асессора

Сервис разрабатывается [v-team SinSig](https://abc.yandex-team.ru/services/sinsig/).

## Быстрый старт

- Установить nvm (node version manager) и переключиться на нужную версию NodeJS:

  ```$ nvm use```

- Установить зависимости:

  ```$ npm ci```
- Настройка локального TVM:

  Посмотреть [тут](https://yav.yandex-team.ru/secret/sec-01eac8944ee1rw34pxteb8v45e/explore/version/ver-01eac8944vvpwfvcd40rx6ckfp) секрет для TVM. Если доступа нет, обратитесь к TVM-менеджеру [сервиса](https://abc.yandex-team.ru/services/sinsig/).

  Выполнить:

  ```$ TVM_SECRET=<секрет из ссылки> npm run tvm:init```
- Запуск проекта:

  ```$ npm run tvm```

  ```$ npm run start```

N.B.: сейчас при локальной разработке поход в черный ящик замокан и возвращает логин, соответствующий
имени пользователя, под которым вы залогинены в своей ОС. Логин можно переопределить, задав переменную окружения ```STUB_USERNAME```.

## Тесты

### Unit

Для юнит-тестов используется Jest + Enzyme (для снэпшот-тестирования реакт-компонентов). Файлы с тестами имеют расширение .spec.ts(x).

Юнит-тесты используются в ci (```$ npm run ci:unit```)

Запуск тестов:

```$ npm run unit```

Обновление снепшоотов компонентов:

```$ npm run unit -- -u```

### E2E

E2E-тесты с использованием гермионы лежат в папке ```tests/e2e/hermione```
и проверяют окружение <https://test.myexpert.yandex-team.ru>.

Тест-кейсы описаны в [testpalm](https://testpalm2.yandex-team.ru/sinsig-myexpert).

Тесты запускаются раз в сутки [шедулером](https://sandbox.yandex-team.ru/scheduler/22760/view), письма с отчетами
о результатах приходят на [рассылку](https://ml.yandex-team.ru/lists/myexpert-front).

Ручной запуск тестов на локальной машине (используется удаленный грид):

```$ npm run hermione:e2e```

## Сборка докер-образов

Образы хранятся в [registry](https://wiki.yandex-team.ru/qloud/docker-registry/) в репозитории mm-interfaces/sinsig-assessors (registry.yandex.net/mm-interfaces/sinsig-assessors).

Для работы с registry нужно:

1. Установить docker
2. Получить [по инструкции](https://wiki.yandex-team.ru/docker-registry/#authorization) токен
3. ```$ docker login -u <логин на staff> -p <полученный токен> registry.yandex.net```

Для сборки докер-образов существуют вспомогательные скрипты:

- ```$ npm run docker-build-release``` – собирает образ и проставляет тег, соответствующий версии в package.json
- ```$ npm run docker-build-latest``` – собирает образ и проставляет тег latest
- ```$ npm run docker-publish-release``` - то же, что build-release, но дополнительно пушит образ в репозиторий
- ```$ npm run docker-publish-latest``` - то же, что build-latest, но дополнительно пушит образ в репозиторий

Можно указать любой тег образа через переменную DOCKER_IMAGE_TAG:

```$ DOCKER_IMAGE_TAG="<tag>" npm run docker-build```

```$ DOCKER_IMAGE_TAG="<tag>" npm run docker-push```

## Деплой

Сервис живет в Yandex Deploy: <https://deploy.yandex-team.ru/projects/sinsig-assessors>.

Пока что скриптов для деплоя нет, поэтому нужно сходить в настройки окружения и руками в конфиге прописать нужный образ.

## Мониторинги

### Мониторинг клиентских ошибок

[Посмотреть в Error Booster](https://error.yandex-team.ru/projects/sinsig-myexpert).

### Мониторинги балансера
[Посмотреть в Nanny](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/myexpert.yandex-team.ru/monitoring/common/).

### Обновление настроек алертов

Для настройки алертов используется [monitorado](https://github.yandex-team.ru/toolbox/monitorado).

1. Правим файл конфига (`.config/monitorado/.monitorado.yml`)

2. Устанавливаем monitorado:

        npm i -g @yandex-int/monitorado --registry=https://npm.yandex-team.ru

3. переходим в папку с конфигом `monitorado`

        cd ./.config/monitorado

4. [Получаем токен](https://github.yandex-team.ru/toolbox/monitorado#%D0%A2%D0%BE%D0%BA%D0%B5%D0%BD%D1%8B) и кладем в файл `.env`

5. Смотрим diff:

        monitorado diff -v

6. Обновляем конфиг:

        monitorado exec -v

## Ссылки на окружения

- <https://myexpert.yandex-team.ru> – продакшн
- <https://test.myexpert.yandex-team.ru> – тестинг

## Яндекс.Метрика
[Номер счетчика – 68587432](https://metrika.yandex.ru/dashboard?group=day&period=week&id=68587432)
