# Сервис управления соревнованиями площадки Яндекс.Контест

> Make Contest Great Again!

[![oko health](https://badger.yandex-team.ru/oko/repo/contest/contest-admin/health.svg)](https://oko.yandex-team.ru/repo/contest/contest-admin)

- [Подготовка](#Подготовка)
- [Установка и запуск](#Установка-и-запуск)
- [Вопросы безопасности](#Вопросы-безопасности)
    - [Закрываем хэлсчеки от внешних пользователей](#Закрываем-хэлсчеки-от-внешних-пользователей)
    - [Делимся секретами для локальной разработки с командой](#Делимся-секретами-для-локальной-разработки-с-командой)
- [Интернационализация](#Интернационализация)
    - [Сборка](#Сборка)
    - [Ключи в Танкере](#Ключи-в-танкере)
    - [Как использовать](#Как-использовать)
        - [Как функция](#Как-функция)
        - [Как компонент](#Как-компонент)
- [Мониторинги](#Мониторинги)
- [Доступные команды](#Доступные-команды)
- [Документация](#Документация)

## Подготовка

Для работы потребуется Node.js 12.18.1.

Для начала [устанавливаем nvm](https://github.com/nvm-sh/nvm#install--update-script). Затем:

```bash
# Устанавливаем Node.js 12.18.1 версии
nvm install 12.18.1
```

## Установка и запуск

```bash
# Устанавливаем зависимости
npm run deps

# Запускаем приложение (magicdev запросит ваш пароль, чтобы запустить его на 443 порту).
# По необходимости, вы может задать другой порт, не требующий sudo, в файле .magicdev.json.
npm run dev

# Можно также запускать со сборкой в нескольких локалях
BUILD_LANGS=1 npm run dev
```

Проект становится доступен по адресу:
https://localhost.msup.yandex.ru:8443/

## Локальный запуск тестов
Hermione тесты запускаются на storybook через selenium grid.
Тесты запускаются на сбилженную статику сторибука.
Поэтому непосредственно перед запуском тестов надо собрать сторибук

Для локального тестирования выполните следующее
```bash
npm run storybook:build:hermione
# для запуска тестов с gui
npm run hermione:gui
# для запуска тестов без gui
npm run hermione:test
```

## Логи
Клиентские ошибки в [ErrorBooster](https://error.yandex-team.ru/projects/contest-admin)

## Релиз
### Выкатываем релиз
[вики](https://wiki.yandex-team.ru/bliss/monorepo/release/#zavodimreliz)
1. Убедиться, что все фичи, необходимые для релиза находятся в `trunk`-ветке
1. Открыть [форму отведения релизов](https://forms.yandex-team.ru/surveys/50569/)
1. В "Название сервиса" указываем `contest-admin`, ниже выбрать "Внеплановый релиз" и жмем "Запустить релиз"
1. Стартанет sandbox таска, которая заведет релизный тикет в очереди [SEAREL](https://st.yandex-team.ru/SEAREL) и запустит выкатку релиза на prestable (ссылка на trendbox таску будет в комментариях)
1. Дождаться окончания выкатки (о результате будет отписано в комментариях)
1. Проверить на https://admin.contest.prestable.yandex.ru что релиз не падает
1. Взять с [prestable](https://deploy.yandex-team.ru/stages/contest-admin-prestable/config/du-frontend/box-frontend) тег docker image и выкатить его в [production](https://deploy.yandex-team.ru/stages/contest-admin-production/edit/du-frontend/box-frontend)
1. Дождаться раскатки. Во время раскатк следить за [логами](https://deploy.yandex-team.ru/project/contest-admin-production/logs) 
и [мониторами](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=contest-frontend-ext.yandex.net;itype=balancer;ctype=prod;locations=msk,sas,vla;prj=contest-frontend-ext.yandex.net;signal=admin-main;)
1. Проверить, что сервис работает
1. Перевести релизный тикет в статус "Закрыт (Решен)"

### Если релиз отвели и в него надо внести правки
Смотри в [вики](https://wiki.yandex-team.ru/bliss/monorepo/release/#zavodimreliz)

### Если релиз отвели и решили не релизить
[вики](https://wiki.yandex-team.ru/bliss/monorepo/release/#otvelirelizireshilipokanerelizit)
1. Перейти в релизный тикет и закрыть его с резолюцией "Некорректный"



## Вопросы безопасности

### Закрываем хэлсчеки от внешних пользователей

Из коробки стаб предлагает хелсчеки для отслеживания состояния необходимых смежных сервисов (например, доступность чёрного ящика, геобазы и базы данных). Пути, за которыми они скрыты, могут быть использованы для создания HTTP juggler-проверок в Qloud.

> :warning: Для того, чтобы эти пути не стали доступны внешним пользователям на публичном домене, необходимо в Qloud создать путь `/healthchecks/` и направить его в компоненту типа _http-balancer_, в параметре _Servers_ указав `http://any.yandex.ru/`.

### Делимся секретами для локальной разработки с командой

Для доступа к ЧЯ при локальной разработке в корень проекта необходимо положить файл [.tvm.json](https://yav.yandex-team.ru/secret/sec-01d7c7xjv4yqyaep4ddx5hk3cs)

Для локальной работы с S3 необходимо сохранить в корне проекта файл `.env`, в котором должны быть указаны реквизиты доступа:
```
AWS_SECRET_ACCESS_KEY=xxxx
AWS_ACCESS_KEY_ID=xxxx
```
Данные ключи находятся [в секретнице](https://yav.yandex-team.ru/secret/sec-01dd3aq5j9bqcxyn9sg9xx5ze2)


## Интернационализация

### Сборка

Для каждого языка собирается отдельный бандл.
Список языков для которых осуществляется сборка указан в файле *configs/defaults.ts*.

> :bulb: При наличии включенной переменной `BUILD_LANGS` можно собрать все языки, т.е. можно запустить
сервер командой `BUILD_LANGS=1 npm run dev` и собираться будут бандлы всех языков

> :bulb: Для ускорения локальной разработки этот список можно сократить в файле *configs/local.ts*

Чтобы скачать актуальное состояние переводов из танкера, выполните `npm run i18n:download`.

### Ключи в Танкере

Параметры в теле ключа должны быть в формате `{param_name}`.
Для выбора правильного склонения **plural** ключа используется специальный параметр `count`.

### Как использовать

#### Как функция

```typescript jsx
import i18n from 'client/utils/i18n';

// Результат вызова этой функции - строка
// Эта функция особенно полезна в случае если нужно передать именно строку
// Например placeholder в <input />
const string = i18n.text({
    key: 'key_id',        // Идентификатор ключа в Танкере
    keyset: 'keyset_id',  // Идентификатор кейсета в Танкере
    params: {             // В качестве параметров могут быть только строки или числа
        param_1: 'value_1',
        param_2: 'value_2'
    }
});

// Результат вызова этой функции - ReactElement
// Полезно если в качестве параметров хочется использовать компоненты
// Или если необходимо вставить контент без экранирования
const reactElement = i18n.element({
    escape: true,          // Нужно ли экранировать содержимое ключа и параметров (По умолчанию `false`)
    key: 'key_id',
    keyset: 'keyset_id',
    params: {              // В качестве параметров может быть что угодно, что может отрендерить React
        param_1: 'value_1',
        param_2: <button>Click me</button>
    }
});
```

#### Как компонент

```typescript jsx
import I18N from 'client/components/i18n';

<I18N
    escape
    id="key_id" // Используется атрибут "id" т.к. "key" в React зарезервирован
    keyset="keyset_id"
    param={{
        param_1: 'value_1',
        param_2: <button>Click me</button>
    }}
/>
```

### Feature-флаги
В проекте существует возможность уносить функциональность под флаг (то есть получить возможность катить фичи только на тестинг и отключать их для той же сборки в проде). 
Для этого нужно в конфиге соответствующего окружения добавить флаг с булевым значением "Включить/выключить функциональность для данного окружения. Например:
```javascript
// configs/testing.ts
{
    features: {
        'my-asesome-feature': true
    },
    ...otherConfig
}
```

После тестирования функциональности можно быстро ее включить в продакшне, выставив этот же флаг в конфиге `configs/production.ts`. 
Для того, чтобы получить доступ к флагу на клиенте необходимо заиспользовать контекст `UserFeaturesContext`. Например:
```javascript
import { MY_AWESOME_FEATURE } from 'common/features'; // export const MY_AWESOME_FEATURE = 'my-awesome-feature';

// ...
    <UserFeaturesContext.Consumer>
        {features => features[MY_AWESOME_FEATURE] ? 'enabled' : 'disabled'}
    </UserFeaturesContext.Consumer>
// ...
```

### Runtime-параметры рендеринга

Для передачи динамических параметров, которые хочется менять на лету (с помощью переменных окружения) предусмотрена переменная окружения `RENDER_PARAMS`, которая принимает
в качестве значения JSON-строку. Важно стараться избегать использования данного инструмента, поскольку легко допустить ошибку при создании данной JSON-строки.

#### Текущие Runtime-параметры

— `disableOldAdminRedirects` — позволяет отключать редиректы в старую админку


## Доступные команды

Команда | Действие
------------ | -------------
deps | Установка зависимостей
dev | Запуск tvmtool и приложения для локальной разработки
build | Запуск production сборки скриптов и стилей
lint | Проверка TypeScript и CSS кода на codestyle
test | Запуск тестов 


## Документация

* [Гайды по использованию проектов на основе Project Stub](https://wiki.yandex-team.ru/toolbox/project-stub/)

## Troubleshooting


1. После переустановки зависимостей начали отваливаться типы. Часто бывает с `@types/node`  
Solution: Запустить `npm dedupe`
