# Интерфейс администратора сайта Математического конгресса

Шабллон проекта на [Next.js](https://nextjs.org/)

## Устанновка

[Как установить brew](https://wiki.yandex-team.ru/spec/devops/kakustanovitbrew/)

```bash
# Устанавливаем NVM (не забываем выполнить инструкции от Brew в секции Caveats)
brew install nvm

# Устанавливаем Node.js 12 версии
nvm install 12

# Устанавливаем зависимости монорепозитория
cd frontend
npm i

# Устанавливаем зависимости сервиса
cd services/mathcongress-admin
nvm use
npm run deps

# Задаём переменную окружения для локальной разработки
export NODE_ENV=development
```

Добавляем домен для локальной разработки в `/etc/hosts`

```
# Mathcongress
127.0.0.1   local.icm2022.yandex-team.ru
::1         local.icm2022.yandex-team.ru
```

Сохраняем ключи SSL в файлы `ssl/certificate.pem` и `ssl/private_key.pem` из [секрета](https://yav.yandex-team.ru/secret/sec-01eewkrk70bw40jqg5zyhzc89g).

Сохраняем в корень проекта файл `.tvm.json` и подставляем в поле `secret` значение из [client_secret](https://abc.yandex-team.ru/services/mathcongress/resources/?view=consuming&layout=table&supplier=14&show-resource=30378897).

```json
{
    "BbEnvType": 1,
    "clients": {
        "mathcongress-admin": {
            "secret": "XXX",
            "self_tvm_id": 2027836,
            "dsts": {
                "blackbox": {
                    "dst_id": 223
                },
                "api": {
                    "dst_id": 2027826
                }
            }
        }
    }
}
```

## Разработка

```bash
# Локальный запуск
npm run dev
```

:warning: Для доступа в интерфейс требуется роль в IDM: https://nda.ya.ru/t/7NDa6qR_3WVQad

Сервис становится доступен по адресу: https://local.icm2022.yandex-team.ru

##Сборка

### Testing

Приложение выкатывается **автоматически** в тестовое окружение после успешного merge в `trunk`.
Версия приложения соответствует версии в `package.json`. Она так же изменяется **автоматически** - увеличивается минорная версия ([подробнее о правилах версионирования для `/services/*`](https://a.yandex-team.ru/arc_vcs/frontend/docs/faq/packages-autopublish.md#особенности-версионирования-сервисов--services--4)).

Если возникает необходимость собрать версию вручную (локально), это можно сделать с помощью команды

```
npm run tools:deploy
```

Скрипт подскажет, какие переменные окружения необходимо установить. Все переменные окружения, кроме `VERSION`, хранятся в [секретнице](https://yav.yandex-team.ru/secret/sec-01e8ycm1sh4q6ma7jrejjt7dhr/).

Задать переменные окружения:

```bash
export VERSION=xx.y
```

Собранный образ руками выкатывается в testing через интерфейс YD.

### Production

Выкладка на prod происходит в ручном режиме - через интерфейс YD.

### Плагины VSC

-   [EditorConfig](https://marketplace.visualstudio.com/items?itemName=editorconfig.editorconfig)
-   [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)
-   [StyleLint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)
-   [PostCSS Language Support](https://marketplace.visualstudio.com/items?itemName=csstools.postcss)
-   [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

## Синхронизация переводов

Для загрузки и обновления переводов используется пакет [`tanker-kit`](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tanker-kit). Для его работы требуется установить в переменную OAuth-токен: https://nda.ya.ru/3SjQY7

```bash
export TANKER_OAUTH_TOKEN=xxxx;

npm run tanker:pull # Выгрузить переводы
npm run tanker:push # Загрузить переводы
```

## Design by Contract

Рядом с приложением поднимается DbC-сервер, расположенный в файле `contract-server.ts`. Именно к этому серверу приложение обращается за данными при локальной разработке. Конфигурация обработчиков запросов является контрактом для проектирования бэкенда.

Поднять сервер локально можно при помощи коанды `npm run start:contract`, после чего он станет доступен по адресу http://localhost:8080/v1/ping.

## Документация

Актуальная информация по проекту [находится на wiki](https://wiki.yandex-team.ru/bliss/mathcongress/)
