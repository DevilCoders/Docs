# Фемида

[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend/services/femida&vcs=arc)](https://oko.yandex-team.ru/arc/frontend/services/femida)

### Quick start
```
npm ci
npx make-my-env
npm run build:dev
npm run dev
```

### Запуск с вотчером
```
npm run dev
BUNDLES="main femida" LANGS=ru npm run dev
```
:exclamation: Вотчер следит только за изменениями в блоках (`/blocks/*`, `bundles/*/blocks/*`, `/src/*`), если изменились модели, сборку нужно перезапускать вручную.

### Cоздание компонента

Для создания новых **компонентов/элементов/модификаторов/сторибуков** нужно пользоваться командой, которая автоматически сгенерирует все необходимые файлы

```
npm run generate
```

Команда предложит выбор и попросит ввести названия компонентов/элементов/модификаторов

*Команду нужно использовать как для новых, так и для текущих компонентов*

### Создание нового бандла
1. В файле /bundles.json создаем новую запись. Циферку для RUM-счетчика берем [отсюда](https://stat.yandex-team.ru/DictionaryEditor/BlockStat), возможно нужно будет создать предварительно запись.
2. В src/bundles создаем входные точки для ru и en. Здесь нужна будет оптимизация чтобы избежать дублирования, но пока так.
3. В static/bundles/<name> создаем файл <name>.bemdecl.js. Это нужно, чтобы работала сборка (она одновременно собирает легаси бем-код и новый реакт, потому нужны вот такие приседания)
4. Если нужно, настраиваем .config/archon/components/applications.js, который запускает наше приложение для hermione-тестов

### Как работает

* `/blocks/*` — блоки проекта
  * `/blocks/crutches/*` — костыли, которые должны быть выброшены с обновлением чего-либо
  * `/blocks/desktop/*` — основные блоки
  * `/blocks/external/*` — переопределения внешних (библиотечных) блоков
* `/modules/*` — модули проекта
* `/static/bundles/*` — бандлы
* `/static/bundles/*/blocks/*` — блоки бандла
* `/static/bundles/*/modules/*` — модули бандла бандла

:exclamation: Бандл с вакансиями называется positions, потому бандлы, начинающиеся с `v`, неправильно обрабатываются в qloud cdn.

### Хостинг

Статика фронтенда хранится на S3. При сборке проекта генерируется файл `manifest.json`, который содержит пути до всех файлов проекта. Сам `manifest.json` хранится в S3 за версией проекта. Пример: `https://femida.s3.mds.yandex.net/femida/3.591.0/manifest.json`. Таким образом каждой версии проекта соответствует один `manifest.json`

[Бэкенд Фемиды](https://deploy.yandex-team.ru/projects/femida) раздает index.html для каждой страницы и подставляет пути до статики из `manifest.json`, который загружает для версии, указанной в поле `FRONTEND_VERSION` в админке

[Админка тестинг](https://femida.test.yandex-team.ru/admin/constance/config/)
[Админка прод](https://femida.yandex-team.ru/admin/constance/config/)

### Автотесты

Для инфраструктуры тестов используется связка clement + tunneler + hermione.
Тесты гоняются на машинках https://selenium.yandex-team.ru, и пока что живут в общей квоте selenium.

[Схема работы](https://media.github.yandex-team.ru/user/6722/files/37e0dd00-37a0-11ea-8c4e-c9313148967a)

Шедулер для выгрузки статистики по фичам: https://sandbox.yandex-team.ru/scheduler/23587/view

Шедулер для выгрузки основной статистики: https://sandbox.yandex-team.ru/scheduler/17504/view

#### Запуск

`npm run build:dev` - сборка проекта
`npm run test:hermione` - запустить все тесты Гермионы в консоли без gui
`npm run test:templates` - тесты на шаблоны [enb-bem-tmpl-specs](https://github.com/enb/enb-bem-tmpl-specs)

#### Разработка

* Запуск с использованием отличного от тестового стенда бека:

    `STAND=prefix npm run dev` где `${prefix}.femida.test.yandex-team.ru`. К примеру `STAND=qazaq npm run dev` для использования стенда `qazaq.femida.test.yandex-team.ru`

    `BACKEND=full_backend_name npm run dev` где `full_backend_name` это полный аддрес бека. К примеру `BACKEND="qazaq.femida.test.yandex-team.ru" npm run dev` для использования стенда `qazaq.femida.test.yandex-team.ru`

* Перезапись шаблонов (отображает ошибки -- это норма):
   `BEM_TMPL_SPECS_SAVE_REFERENCE_HTML=1 npm run test:templates`

* Запуск тестов в режиме графического интерфейса:
    `npm run test:hermione -- --gui`

* Запустить тесты с `vnc`, дает возможностью управлять удаленным браузером. Чтобы было удобнее дебажить конкретное место в тесте, можно ставить `.debug()`:
   `npm run test:hermione -- -b yandex-browser-desktop --debug --debug-vnc-before-test 1 --debug-no-timeouts 1 --debug-pause-on-vnc 1`

* Отображение отчёта о пройденных тестах в браузере:
   `npm run test:hermione -- --gui hermione/tests/desktop/vacancies/vacancies_create/vacancies_create.hermione.js -a`

* Прогон тестов в режиме create элемента:
   `npm run test:hermione -- --gui --mode=create hermione/tests/desktop/vacancies/vacancies_create/vacancies_create.hermione.js --retry=1 -a`

* Скачать отчёт из PR (например для обновления эталонов)
    `npm run test:hermione -- --gui --from https://proxy.sandbox.yandex-team.ru/1490642585/index.html`

Если тесты падают с ошибкой `cannot find module .build/Release/png_img`, может помочь выполнение команды `npm ci`.

### Релизы
Релизы осуществляются по общему монорепозиторному флоу:
1) [Описание релизного процесса сервисов в монорепозитории](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/docs/faq/release-workflow.md)
2) [Подключение автоматизации релизов](https://a.yandex-team.ru/arc_vcs/frontend/docs/how-to/arc/setup-releases.md)
3) [Конфигурация релизов](https://docs.yandex-team.ru/ci/release)

#### Расписание

Релизы отводятся с понедельнка по пятницу с 04:00 до 07:00 MSK

Внеплановый релиз можно сделать через [CI](https://a.yandex-team.ru/projects/frontend/ci/releases/timeline?dir=frontend%2Fservices%2Ffemida&id=release)

[Как отвести релиз](https://a.yandex-team.ru/arc_vcs/frontend/docs/how-to/arc/setup-releases.md#отведение-релиза-из-ci)

#### Выкатка в прод

Для релиза в прод нужно взять версию из поля `FRONTEND_VERSION` в админке тестинга и сохранить ее в админке продакшена. Url админки смотри в пункте [хостинг](#хостинг)

### Стенды

На ПР автоматически поднимается стенд, глядящий в тестинг бэкенда.

Если надо перенаправить стенд на другой бэкэнд, нужно заменить адрес бэкенда в конце ссылки на адрес стенда.

Например:
```
https://femida-front-pr-2546336-1.femida.test.yandex-team.ru/ - смотрит в тестинг бэкенда
https://femida-front-pr-2546336-rpl5.femida.test.yandex-team.ru/ - смотрит в стенд rpl5
```

Список доступных стендов [тут](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/femida.test.yandex-team.ru/backends/list/)

### Деплой

Если вдруг нужно зарелизиться руками, то:

1. Собрать и залить статику на S3:

   - `arc checkout trunk && arc pull trunk`

   - `npm run ci:deploy:release`

2. После успешной загрузки на S3 нужно пойти в админку и проставить версию из `package.json` в поле `FRONTEND_VERSION` в админке. Url админки смотри в пункте [хостинг](#хостинг)


#### Секреты и получение доступа к S3

* Вы можете взять готовые секреты для пользователя `robot-mop` в [yav](https://yav.yandex-team.ru/secret/sec-01dgzacpdyjq7pp6yf8n79d45b/explore/versions).

* За Фемидой закреплены два бакета `femida` и `femida-ext` (сейчас используется только femida-ext, он доступен наружу, второй лежит на случай если мы будем закрывать нашу статику от внешних пользователей, для них как раз останется femida-ext).

* Для получения персонального доступа к бакетам, нужно сделать запрос в [IDM](https://idm.yandex-team.ru/#rf-role=hXo0ds2c#s3-mds/femida-825-37154/service-account-role/admin;;;,rf-expanded=hXo0ds2c,rf=1). И далее выполнить шаги описанные [здесь](https://wiki.yandex-team.ru/mds/s3-api/authorization/#sozdanieaccesskey). Еще один [секрет](https://yav.yandex-team.ru/edit/secret/sec-01dgza7hhqq8yvcjgwnd6ks09j/explore/versions) robot-mop (нужен только в целях перезапроса ключей `S3_ACCESS_KEY_SECRET` `S3_ACCESS_KEY_ID`).

### RUM (Скорость интерфейсов)

[Дашборд с графиками скорости](https://datalens.yandex-team.ru/6egfqynhinvm1-femida-speed)
[Риалтаймовые графики](https://rum.yandex-team.ru/projects/femida)

`RUM_COUNTER_DEBUG=1 npm run dev` - запустит локальную разработку в режиме дебага rum счетчиков.
Можно проверить какие счетчики будут отправлены при загрузке страницы, данные отображаются в консоли браузера.

### Решение проблем

#### 1. Не отправляется локально форма, 403, проблема с csrf

Открыть в браузере ссылку https://femida.local.yandex-team.ru/api/_meta и попробовать ещё раз отправить форму.

В чём магия? Всё просто - в тестинге/продакшене бэкенд при формировании html инициализирует csrf для форм обращаясь к ручке `/api/_meta`.
