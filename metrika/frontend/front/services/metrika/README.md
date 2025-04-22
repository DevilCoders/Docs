# Metrika Frontend

- [Планирование](https://wiki.yandex-team.ru/jandexmetrika/frontend/planning/) | [Дашборд задач спринта](https://st.yandex-team.ru/agile/board/9501)

- [Инструкция для дежурного по ZBP](https://wiki.yandex-team.ru/JandexMetrika/Frontend/Инструкция-для-дежурного-по-ZBP/) |  [Дашборд ZBP](https://st.yandex-team.ru/dashboard/53103)

- [Список актуальных дежурных](https://duty.mtrs.yandex-team.ru/project/metrika/)

- [Главная фронтовая Wiki страничка](https://wiki.yandex-team.ru/jandexmetrika/frontend/)

- [Чаты аналитических продуктов](https://wiki.yandex-team.ru/jandexmetrika/chats/)

## Документация

- [Bem Node](https://github.com/bem-node)
- [Metrika BEM](https://github.yandex-team.ru/ilyakortasov/my-stuff/blob/master/metrika-bem.md#metrika-bem)
- [i-bem / islands](https://islands-lego.yandex-team.ru/libs/islands/v6.5.0/desktop/i-bem/jsdoc/)
- [Яндекс Лего](https://lego.yandex-team.ru/)
- [Работе с данными marketplace](https://a.yandex-team.ru/arc_vcs/metrika/frontend/front/services/metrika-bem/tools/marketplace-data/README.md#здесь-лежат-данные-для-маркетплейса)

## Разработка

1) Заводим виртуалку [по инструкции](https://wiki.yandex-team.ru/JandexMetrika/frontend/dev_computer_for_everyone/)

2) Устанавливаем [инстурменты разработчика](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)

3) Добавляем плагин в IDE для синхронизации с виртуалкой:

   - [Remote SSH для VS Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)

3) Ставим зависимости и запускаем:
```
cd ~/arcadia/metrika/frontend/front
npm run bootstrap:metrika

cd ~/arcadia/metrika/frontend/front/services/metrika
BUNDLES=common,tags LANGS=ru make compose-up
```

Другие сервисы (appmetrica, radar, audience) запускаются по аналогии, но для них можно не указывать бандлы, потому что их там гораздо меньше и они почти не влияют на скорость сборки

Как правило, common и tags достаточно, иначе добавляем другие бандлы в сборку. [Полный список бандлов](https://a.yandex-team.ru/arcadia/metrika/frontend/front/services/metrika-bem/pages-desktop/metrika)

Также есть разделение на БЭМ и React страницы. Что и куда ведём можно узнать в [конфиге nginx](https://a.yandex-team.ru/arc_vcs/metrika/frontend/front/services/metrika/nginx/conf.d/default.conf.template)

### Смена окружения через Bishop

Требуется, когда надо подключиться к тестовому хосту API и т.д.

- [Инструкция по работе с Bishop](https://a.yandex-team.ru/arcadia/metrika/frontend/front/docs/manual/bishop.md)
- [Сылочки на наши окружения](https://a.yandex-team.ru/arcadia/metrika/frontend/front/services/metrika/README.md#infrastruktura)

Для переключения на другое окружение меняем в файле [docker-compose.yml](https://a.yandex-team.ru/arcadia/metrika/frontend/front/services/metrika/docker-compose.yml) значения `BISHOP_ENVIRONMENT_NAME` для разных сервисов

### Темизация

Есть [отдельное README](https://a.yandex-team.ru/arc_vcs/metrika/frontend/front/packages/contrib/ui/theme/README.md#темизация)

## Тестирование
- [Данные для тестирования](https://wiki.yandex-team.ru/testirovanie/functesting/advtechnologies/metrikadata/) — когда нужен *счетчик с определенной фичей* или *логин с определенной ролью*
- [BrowserStack](https://wiki.yandex-team.ru/jandexmetrika/frontend/browserstack/) — проверка на разных устройствах

## Релиз
- [Подробное описание на Wiki](https://wiki.yandex-team.ru/JandexMetrika/frontend/release_process/)
- [Метрика. UI Release Dashboard](https://st.yandex-team.ru/dashboard/7162)

## Графики
- [Juggler](https://juggler.yandex-team.ru/dashboards/metrika_frontend/) | [Графики](https://yasm.yandex-team.ru/panel/robot-metrika-admin.metrika-awacs-metrika.yandex.ru-service_backends_total-ALL-main-dashboard/)
- [Faced](https://grafana.yandex-team.ru/d/8POzZXEGz/metrika-faced-in-deploy) | [API Balancers](https://grafana.yandex-team.ru/d/8afaZM_Mz/metrika-and-appmetrika-api-balancers)
- [Error Booster](https://error.yandex-team.ru/projects/metrika/)
- МongoDB
	- [Кластер целиком](https://yc.yandex-team.ru/folders/foori5uktoh2v12cbltq/managed-mongodb/cluster/mdbjl5fcfsogbptvd1an?section=monitoring)
	- [Данные отдельных хостов](https://yc.yandex-team.ru/folders/foori5uktoh2v12cbltq/managed-mongodb/cluster/mdbjl5fcfsogbptvd1an?section=hosts&hostName=man-o7mv9cwso43xktil.db.yandex.net)
	- [Список долгих запросов MongoDB](https://grafana.yandex-team.ru/d/NB7iQI_Mk/mdb-managed-mongodb-perfdiag-overview?orgId=1&var-cid=mdbjl5fcfsogbptvd1an), подробнее про него [вот здесь](https://clubs.at.yandex-team.ru/mdb/763)

Кое-что настроено через [Monitorado](https://a.yandex-team.ru/arc_vcs/frontend/packages/monitorado), актуальный конфиги лежат в [contrib/utils-configs/monitoring](https://github.yandex-team.ru/Metrika/frontend/blob/develop/packages/contrib/utils-configs/monitoring/.monitorado.yml)


## MongoDB

Метрика и АппМетрика живут в разных базах одного кластера MDB:
- [metrika-test](https://yc.yandex-team.ru/folders/foori5uktoh2v12cbltq/managed-mongodb/cluster/mdbsvr7rqlh3jj2arjc6)
- [metrika-prod](https://yc.yandex-team.ru/folders/foori5uktoh2v12cbltq/managed-mongodb/cluster/mdbjl5fcfsogbptvd1an)

Для работы с Монгой есть скрипты для подключения, синхронизации и миграции

Их надо запускать из `packages/contrib`

```
cd packages/contrib
```

### Подключиться к базе через консоль

На тестовой базе мы можем и читать и писать, но при подключение к проду будут read-only права

```
$ npm run mongo:connect:metrika -- --env [test|prod]

# пример
npm run mongo:connect:metrika -- --env test
```

### Синхронизация тестинга с продом

Добавить коллекцию в [список для синхронизации](https://github.yandex-team.ru/Metrika/frontend/blob/develop/packages/contrib/utils-configs/mongo/data.ts#L11), если она там отсутствует, а затем запустить скрипт синхронизации

```
$ npm run mongo:sync:metrika -- --collection [col1 col2 ...] --pathToDump [folder]

# пример
npm run mongo:sync:metrika -- --collection widgets2 --pathToDump ~/dump
```

В скрипте лучше явно указывать куда сохранить коллекцию, чтобы потом её можно было удалить и освободить место на диске, потому что коллекции в Монге могут весить десятки гигабайт. Если папка с указанным именем отсутствует, то Монга создаст её за нас

### Миграция

Для миграции используем [Migrate Mongo](https://github.com/seppevs/migrate-mongo#basic-usage)

Чтобы мигрировать данные, в папке `migrations` требуется создать файл с помощью скрипта
```
npm run mongo:migrate:metrika:create -- --name=MIGRATION_NAME
```
Название `MIGRATION_NAME` будет соответствовать номеру тикета, например, `metr-31415`.

В созданном файле нужно описать миграцию данных, закоммитить вместе с задачей, а затем вручную раскатить через специальный скрипт для тестинга и прода по мере тестирования и выкладки новой фичи

Формат файла можно посмотреть в предыдущих миграциях или в [документации](https://github.com/seppevs/migrate-mongo#example-2-use-async--await)


Описание скрипта:

```
$ npm run mongo:migrate:metrika -- --env [test|prod] --command [list|up|down]

# пример
npm run mongo:migrate:metrika -- --env test --command list
```

Пояснение команд:
- __list__ - список всех миграций. Если миграция ещё не раскатана, то она помечается как PENDING, иначе выводится дата и время выкатки
- __up__ - раскатить все миграции, которые еще не были запущены
- __down__ - последовательно по одной откатывать миграции в том порядке, в котором они раскатывались

## Инфраструктура
- [Deploy](https://deploy.yandex-team.ru/) — виртуальные поды в облаках
- [Секретница](https://yav.yandex-team.ru/) — хранилище для секретов. Чаще всего требуется заглядывать вот сюда:
	- [metrika-frontend-testing](https://yav.yandex-team.ru/secret/sec-01dc2e47bg95qvz40g9jx9p5gs/explore/versions)
	- [metrika-frontend-production](https://yav.yandex-team.ru/secret/sec-01dc2dvq8yndznpdschgx7zks9/explore/versions)
- Bishop — настройка конфигов.
	- metrika-bem
		- [Program](https://bishop.mtrs.yandex-team.ru/program/metrika-bem-frontend)
		- [Template](https://bishop.mtrs.yandex-team.ru/template/metrika-bem-frontend.yaml)
		- [Environment (develop)](https://bishop.mtrs.yandex-team.ru/environment/metrika.deploy.frontend.metrika-bem.testing.development)
	- metrika (react)
		- [Program](https://bishop.mtrs.yandex-team.ru/program/metrika-frontend2)
		- [Template](https://bishop.mtrs.yandex-team.ru/template/metrika-frontend2.yaml)
		- [Environment (develop)](https://bishop.mtrs.yandex-team.ru/environment/metrika.deploy.frontend.metrika.testing.development)

### Авто-беты
Создаются автоматически через github хук через [наш собственный сервис авто-бет](https://github.yandex-team.ru/Metrika/frontend/tree/develop/services/autobeta#autobetas), который запускает сборку в Sandbox и пишет комментарий к задаче в Трекере

Удаляются тоже автоматически через 14 дней, либо после вливания или закрытия пул-реквеста

Полезные ссылки:
- [Подробное описание на Wiki](https://wiki.yandex-team.ru/jandexmetrika/frontend/avtobety/)
- [Список всех собранных подов в Deploy](https://deploy.yandex-team.ru/projects/metrika-frontend-autobetas)
- [Задача в Sandbox](https://sandbox.yandex-team.ru/tasks?children=false&type=METRIKA_FRONTEND_DEVELOPMENT&limit=20) — требуется, когда надо вручную создать авто-бету

## i18n
Все переводы хранятся в [Танкере в проекте metrika-bem](https://tanker-beta.yandex-team.ru/project/metrika-bem)

### metrika-bem
Для переводов в БЭМ потребуется создать файл с токеном для авторизации:
```
sudo mkdir -p /home/robot-metrika-test/tanker/
sudo bash -c "echo -n '...' > /home/robot-metrika-test/tanker/.oAuth"
```

Вместо `...` надо скопировать `tanker-token` из [секретницы для robot-metrika-test](https://nda.ya.ru/t/uoPvm0i74wZaLz)

Загрузку переводов выполняем командами:

```bash
# по блоку
npx lerna run i18n --scope=metrika-bem -- -- --blocks='counter-edit'
# по кейсету
npx lerna run i18n --scope=metrika-bem -- -- --keysets='blocks:common:counter-edit'
```

Плюаризация — [динамические ключи в Танкере](https://doc.yandex-team.ru/Tanker/tech-dscr/concepts/tr_keys.html?lang=ru)

### metrika (react)
Для загрузки переводов в React нужен [OAuth токен для Танкера](https://nda.ya.ru/3SjQY7)

Важно! Закомитить все изменения перед загрузкой переводов, потому что подтянуться *переводы всех блоков*

```bash
# экспортируем токен
export TANKER_API_TOKEN="..."
# переходим в папку с проектом
cd services/metrika
# загрузить все переводы разом
npx tanker pull
# ... закомитеть наши блоки
```

[Документация по CLI для tanker-kit](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/tanker-kit/README.md#konsolnyj-interfejs)

Плюаризация — [API для I18N](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/i18n#i18n)

## Код-ревью
Мы используем [яндексовую ревьюшницу](https://github.yandex-team.ru/devexp/devexp#devexp)

- [Developer Dashboard](https://developer-dashboard.yandex-team.ru/) — список твоих пулл-реквестов и ревью
- [Напоминания о ревью](https://github.yandex-team.ru/devexp/devexp#уведомления) на почту, в Telegram или Slack
- [Команды для ревьюшницы](https://github.yandex-team.ru/devexp/devexp#поддерживаемые-команды)

## Дизайн
- [Common Styles](https://www.figma.com/file/08ebVcZomYMGBqMqyN8OGi/Design-Token-Duplo?node-id=0%3A1)


## Тестирование скриншотами

Примере теста для [ErrorMessage](https://github.yandex-team.ru/Metrika/frontend/blob/develop/packages/contrib/ui/components/ErrorMessage/__tests__/ErrorMessage.test.tsx)

Пока что работает только для компонентов внутри `packages/contrib`

### Как добавить

Внутри папки компонента создать директорию `__tests__` и добавить в неё файл в формате `Component.test.tsx`

Затем импортировать компонент с моковыми данными из сторибука и описать тест с `makeScreenshot`:

```
// ... разные импорты

import { makeScreenshot } from '@metrika/ui/utils/jest/makeScreenshot';

import { Component } from '../Component.stories';

describe('Component', () => {
    it('screenshooter', async () => {
        await makeScreenshot(<Component />);
    });
});
```

Дальше перейти в терминале в `packages/contrib` и запустить тест:

```
npm run test -- -t 'Component screenshooter'
```

### Как обновить

Когда какой-то из снапшотов падает — переходим в `Component/__tests__/__image_snapshots__/__diff_output__` и смотрим различия. Затем, либо чиним верстку, чтобы тест проходил, либо обновляем скриншоты. Обновление происходит так же как и для [обычных снапшотов](https://jestjs.io/ru/docs/snapshot-testing) — через флаг `-u`:

```
npm run test -- -t 'Component screenshooter' -u
```

### Как работает

На отдельном [поде](https://deploy.yandex-team.ru/stages/metrika-frontend-screenshooter) запущен [сервис](https://github.yandex-team.ru/telephony/ui/tree/develop/services/screenshot-infra), который принимает разметку, делает скриншот и возвращает картинку

Затем в коде две вспомогательные функции через этот сервис и [jest-image-snapshot](https://github.com/americanexpress/jest-image-snapshot) делают скриншоты:
- [toMatchScreenshot](https://github.yandex-team.ru/Metrika/frontend/blob/94b60c4364a9007bf696690333f81666f0e271ce/packages/contrib/utils-configs/jest/setupTestFramework.ts#L8) — смотрит изменился ли снапшот компонента и при наличие изменений отправляет верстку в сервис скриншутера, получает картинку и сравнить результат через `toMatchImageSnapshot` из [jest-image-snapshot](https://github.com/americanexpress/jest-image-snapshot)
- [makeScreenshot](https://github.yandex-team.ru/Metrika/frontend/blob/94b60c4364a9007bf696690333f81666f0e271ce/packages/contrib/ui/utils/jest/makeScreenshot.ts#L7) —  через `renderToStaticMarkup` формирует верстку для компонента, подтягивает стили из Styled Components, а также css и темизацию для Lego. После чего делает снапшот и вызывает [toMatchScreenshot](https://github.yandex-team.ru/Metrika/frontend/blob/94b60c4364a9007bf696690333f81666f0e271ce/packages/contrib/utils-configs/jest/setupTestFramework.ts#L8)

Когда потребуется подключить скриншутер где-то за пределами `contrib`, достаточно будет переиспользовать логику функций, описанных выше

## Решения проблем

### Ошибка при получении секретов

Выполняем `ssh-add` на ноуте, затем запускаем `eval "$(ssh-agent -s)"` на витуалке, завершаем сессию по `Ctrl + D` и переподключаемся

### Проблемы с arc

Когда появляются ошибки вида:

```
Cannot start service ...: error while creating mount source path '/home/.../arcadia/metrika/frontend/front': mkdir /home/.../arcadia: file exists
```

В этом случае делаем:

```
arc unmount ~/arcadia
arc mount -m ~/arcadia --allow-other --ssh-tokens
```

Возможно, потребутеся ещё запустить:
```
echo "user_allow_other" | sudo tee -a /etc/fuse.conf
arc token store
```



