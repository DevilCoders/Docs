# Дока бывшего Монорепозитория спецпроектов

## Начало работы с монорепозиторием
У Вас должна быть установлена утилита `ya`. Если нет - установите по [инструкции](https://wiki.yandex-team.ru/maps/dev/ui/deploy/yd/#yatool).

Установите зависимости: `make deps`

## Пакеты

~~`./packages` содержит общие пакеты для всех проектов~~

~~Пакеты подключаются в зависимости проектов как локальные зависимости.~~

```
 ~~"dependencies": {~~
   ~~ "@specprojects/bevis": "file:../../packages/bevis"~~
 ~~}~~
```

~~Клиентские зависисмости, которые будут включены в бандл, добавляются в `devDependencies`~~

Все общие пакеты удалены, установка напрямую в проекте

## Проекты

~~Проекты находятся в папке `./projects`, каждый проект в своей папке.
Для создания нового проекта из корня монорепозитория выполните `make project`.~~

Каждый проект живет как отдельный сервис в `maps/front/services`

## Сборка

У каждого проекта свой `Dockerfile` и свой `.qtools.json`.

## Как создать новый проект

1.  Заведите тикет-эпик в очереди `SPGEODEV` по шаблону `Запуск спецпроекта`. Если этого шаблона у Вас нет - добавьте его в настройках Стартрека. Шаблон содержит чеклист запуска нового сервиса. Все дальнейшите тикеты, связанные с этим спецпроектом, линкуйте к эпику.

2. Заведите сервис на [abc](https://abc.yandex-team.ru). Корневой сервис - https://abc.yandex-team.ru/services/maps-front-promo/
Слаг abc - сервиса должен соответствовать маске `maps-front-promo-<your-project-name>`. Например `maps-front-promo-spec-admin`.

3. Если новый сервис будет ходить в другие сервисы Яндекса, создайте TVM - приложения. Abc -> выбрать ваш сервис -> вкладка "Ресурсы" -> кнопка "Запросить ресурс"
-> категория "Безопасность" -> тип "паспорт - tvm приложение". Обычно создают два приложения, для продакшен и для тестинга. После того, как приложения выписались, обязательно пропишите им теги "Продакшен" и "Тестинг" соответственно. В код нельзя коммитить продакшен - секреты, поэтому гит проверят теги секретов tvm и при проверке он смотрит как раз на теги.

4. Если сервис будет использовать Мойру, нужно добавить новый проект в тестовый и продакшн [конфиг Мойры](https://github.yandex-team.ru/maps/moira-int/tree/master/src/app/configs).

5. Если Навигатору нужно узнавать статус пользователя, нужно добавить проект в [продакшин](https://a.yandex-team.ru/arc_vcs/maps/front/services/mobmaps-proxy-api/resources/promodata-config-production.json) и [тестовый](https://a.yandex-team.ru/arc_vcs/maps/front/services/mobmaps-proxy-api/resources/promodata-config-testing.json) конфиг сервиса [mobmaps-proxy-api](https://a.yandex-team.ru/arc_vcs/maps/front/services/mobmaps-proxy-api). В Мойре у пользователя должно быть поле `finished`с булевым заначением.

6. Запросите квоту ресурсов через abc. Для каждого ДЦ должна быть своя заявка.
Сценарий - `Перераспределение ресурсов`. Слаг сервиса-донора - ~~`maps_adv`~~ `maps-front`. Расчет ресурсов: https://wiki.yandex-team.ru/maps/dev/ui/deploy/yd/migration/.edit?section=5&goanchor=capacity. Пример:
```
cpu	1.5
hdd	0.08
ip4	0
net	0
ssd	0
io_hdd	30
io_ssd	0
memory	4
gpu_qty	0
segment	default
location	VLA
scenario	Перераспределение квоты
gpu_model	0
donor_slug	maps_adv
```

### В репозитории
1. Использоват wombat для заведения проекта https://a.yandex-team.ru/arc_vcs/maps/front/tools/wombat
2. Перейдите в директорию нового проекта `cd projects/<your-project>` и выполните команды:
   - `make deps` - установка зависимостей
   - `make local` - подготовка локального окружения
   - `make hosts` - загрузка хостов
3. Пропишите секреты TVM в продакшен и тестинг конфиги Деплоя (`.configs/deploy/testing||production.yml`) в разделах:
   - `tvm_config.clients.secret_selector.alias`
   - `pod_template_spec.spec.secrets`
   - `workloads.app_workload.client_secret`
Вместо плейсхолдеров укажите `secret_uuid` и `version_uuid`. Посмотреть их можно в abc - вкладка "Ресурсы" - выписанный tvm для тестинга или прода. Для просмотра нужны права или руководителя сервиса или TVM менеджера.
4. Запуск проекта локально - `make dev`, приложение доступно по адресу https://localhost:8080/

## Выкладка в тестинг
Домен для тестинга формируется по маске `your-project-name.tst.c.maps.yandex.ru`. Дополнительно прописывать DNS записи не надо, должно работать "из коробки". Если не работает - призовите в тикета devops-а Карт. Дежурные: https://abc.yandex-team.ru/services/maps-front/duty/

1. Поднимите версию приложения ~~`make patch` или `make minor` или `make major`~~ (пока что ручками в файле .qtools.json).
2. Проверьте, что нужные секреты добавлены в конфиги Деплоя, правильно указаны `ID`, `secret_uuid` и `version_uuid` для TVM
3. Для первичной выкладки:
   - В веб-интерфейсе [Deploy](https://deploy.yandex-team.ru) создайте проект. Название проекта должно совпадать со слагом в Abc.
   - из корня проекта выполните `make initial-release-testing`
4. Для повторных релизов в тестинг - `make release-testing`
5. После создания проекта в Деплое, на него нужно выдать права: на всю abc-группу разработки спецпроекта и на abc-группу devops карт `maps-front-infra`. [Пример](https://deploy.yandex-team.ru/projects/maps-front-promo-ingrad), [пример](https://deploy.yandex-team.ru/projects/maps-front-promo-reins-fragile), [пример](https://deploy.yandex-team.ru/projects/maps-front-promo-mts-ecosystem).
5. В [коммунальном тестовом балансере](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-testing.slb.maps.yandex.net) создайте бэкэнды, по одному на каждый ДЦ [пример](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-testing.slb.maps.yandex.net/backends/list/?filter=%7B%22excludeSystem%22:true,%22idRegexp%22:%22ingrad%22%7D).
6. Добавьте новый апстрим в [коммунальный тестовый балансер](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-testing.slb.maps.yandex.net/upstreams/list/)
[Пример](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-testing.slb.maps.yandex.net/upstreams/list/maps-front-ingrad/show/) [пример](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-testing.slb.maps.yandex.net/upstreams/list/maps-front-reins-fragile/show/) [пример](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-testing.slb.maps.yandex.net/upstreams/list/maps-front-promo-mts-ecosystem/show/).
Пример:
```
l7_upstream_macro:
  version: 0.1.0
  id: maps-front-promo-mts-ecosystem
  matcher:
    host_re: mts-ecosystem.tst.c.maps.yandex.ru
  flat_scheme:
    balancer:
      attempts: 2
      max_reattempts_share: 0.2
      max_pessimized_endpoints_share: 0.5
      health_check:
        delay: 5s
        request: >-
          GET /ping HTTP/1.1\nHost:
          front-testing.slb.maps.yandex.net\nUser-agent: l7-balancer\n\n
      retry_http_responses:
        codes:
          - 5xx
      backend_timeout: 300s
      connect_timeout: 0.5s
    backend_ids:
      - maps-front-promo-mts-ecosystem_testing_man
      - maps-front-promo-mts-ecosystem_testing_sas
      - maps-front-promo-mts-ecosystem_testing_vla
    on_error:
      static:
        status: 504
        content: Service Unavailable.
```
Замените `id`, `host_re` и `backend_ids`. В `host_re` укажите ваш домен для тестинга `your-project-name.tst.c.maps.yandex.ru`. Название нового апстрима - `maps-front-promo-{{service-name}}`.

## Выкладка в продакшен
1. Проверьте, что нужные секреты добавлены в конфиги Деплоя, правильно указаны `ID`, `secret_uuid` и `version_uuid` для TVM
2. Для первичной выкладки из корня проекта выполните `make initial-deploy-production`
3. Для повторных релизов в тестинг - `make deploy-production`
4. В коммунальном продакшен балансере ([внутреннем](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-specprojects-int.slb.maps.yandex.net/) или [внешнем](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-specprojects-ext.slb.maps.yandex.net/)) создайте бэкэнды, по одному на каждый ДЦ.
5. Добавьте домен [пример](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-specprojects-ext.slb.maps.yandex.net/domains/list/ingrad-promo.maps.yandex.ru/show/), [пример](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-specprojects-ext.slb.maps.yandex.net/domains/list/mts-cityquest.maps.yandex.net/show/), [пример](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-specprojects-ext.slb.maps.yandex.net/domains/list/renins-promo.maps.yandex.net/show/).
   - `id`: это лейбл, "название" домена. Формируется по маске `*.maps.yandex.net`. Если нужно работать с куками - используйте маску `*.maps.yandex.ru`. Если нужно другое имя, не в неймспейсе `maps.yandex.ru` и `maps.yandex.net`, призовите в тикет [devops-a Карт](https://abc.yandex-team.ru/services/maps-front/duty/), и это желательно сделать заранее.
   - `протоколы`: `HTTP and HTTPS`
   - `FQDNs`: адрес вашего спецпроекта. Формируется по тем же правилам что и `id`.
   - Закажите внешний сертификат для домена. Внешний сертификат буден выдан только после прохождения аудита безопасности. После выдачи, внешний сертификат заработает в течении 48 чассов. Для проверки работоспособности, можно сначала воспользоватся внутренним сертификатом, затем заменить его на внешний.
7. Напишите [дежурному](https://abc.yandex-team.ru/services/maps-front/duty/) devops. Пусть он пропишет DNS и привяжет домен к балансеру.
8. Если нужно матчить разные урлы на разные бэкэнды (например, если у вас апи и приложение находятся в разных приложениях), добавьте апстрим и пропишите в нем правила сопоставления.
9. Перед запуском в продакшен включите мониторинги `npx qtools alerts push --force`


### CI для нового проекта

Проверка конфигурации .trendbox.yml: https://clubs.at.yandex-team.ru/trendbox-ci/223

#### Автоматическая сборка новых версий и выкатка в тестинг

Чтобы насторить автоматическую сборку и деплой в тестинг, в `.trendbox.yml`:

Добавьте `job`:
```
jobs:
   {{yourProject}}release:
      env: SANDBOX_PRIVILEGED_CONTAINER=true
      lifecycle:
         before_install: make docker-login-podrick && make deps && cd ./projects/{{yourProject}}
         install: make deps
         script: make release-testing
```

Добавьте `workflow`:
```
  workflows:
   {{YOURPROJECT}}RELEASE:
      jobs:
         - {{yourProject}}release
```

Добавьте новый триггер, где в фильре укажите префикс проекта в теге версии (см. `Makefile`, команду `.PHONY: patch minor major`)
```
triggers:
   - trigger: tag
      filters:
         events: { only: [created] }
         names: { only: ['{{yourProject}}*'] }
      workflows: {{YOURPROJECT}}RELEASE
```

Теперь на каждый запушенный в гитхаб тег вида `{{yuorProjectName}}-vX.X.X` будет срабатывать джоба `{{yourProject}}release`.


## Автоматическое обновление важных зависимостей

TODO: if it's wanted
~~Файл `.ncurc.json` в корне монорепозитория в ключе `filter` содержит содержит список зависимостей, которые всегда должны быть обновлены до последней версии.

Если аналогичный механизм нужно реализовать внутри спецпроекта:
1. В зависимости проекта добавьте пакет `npm-check-updates`
2. В корень проекта положите файл `.ncurc.json`
3. Из корня проекта выполните `./node_modules/.bin/ncu` / добавьте `make` команду / настройте git - хук~~

## Хранилища
### S3
Внутренний бакет `maps-front-static-int`. Ключ в [секретнице](https://yav.yandex-team.ru/secret/sec-01dmxgnsqbc9enpnt2pcqcj3qd)
### Аватарница
Неймспейс - `maps-front-promo` [тикет](https://st.yandex-team.ru/MDS-11484), [график](https://yasm.yandex-team.ru/template/panel/avatars_mds/ns=maps-front-promo)

Для загурзки картинок в аватарницу используем [upload-api](https://github.yandex-team.ru/maps/upload-api) ([описание ручки](https://github.yandex-team.ru/maps/upload-api/blob/master/docs/v1/spec.yaml#L7)). Пример отправки файла через upload-api в [спецпроекте Уралсиб](https://github.yandex-team.ru/maps/specprojects/blob/8a6c9ff29c1d369dd251cc6eca45d4ff31cd673e/projects/uralsib-admin/src/client/components/pages/moderation-page/moderation-page.tsx#L60).

### Мойра
[Мойра](https://github.yandex-team.ru/maps/moira-int) используется для хранения данных спецпроектов. Внутри доступ к проекту разграницен по `TVM id`.

Для добавления нового проекта в Мойру нужно:
- закоммитить в конфиг новый проект и его `tvm id`. Пример такого коммита [тут](https://github.yandex-team.ru/maps/moira-int/commit/e94ce42085cbd98399deff9705680569590a1a91)
- апнуть версию, выкатить ее в тестинг и продакшен (см. документацию Мойры)

В проектах для взаимодействия с апи Мойры используем модуль `moiraProvider`

### Бункер
Контент для спецпроектов храним в Бункере: https://bunker.yandex-team.ru/maps-promo-specprojects.
Документация Бункера [тут](https://wiki.yandex-team.ru/verstka/tools/bunker/doc-tmp/#schema/create).
Для каждого спецпроекта создаем ноду на верхнем уровне. Имя ноды должно совпадать с слагом проекта на abc. Например `https://bunker.yandex-team.ru/maps-promo-specprojects/maps-front-promo-ingrad`
Схемы данных хранятся в ноде `.schema` на верхнем уровне каждого спецпроекта. Открыть ноду со схемами можно по прямой ссылке, например: `https://bunker.yandex-team.ru/maps-promo-specprojects/maps-front-promo-ingrad/.schema`

## Балансеры
В Деплое в большинстве случаев используем коммунальные балансеры и для тестинга и для продакшена. Если проект сложный / долгий / высоконагруженный, то лучше создать для него отдельный балансер.

| Окружение | Балансер |
|---|---|
| Тестинг | [front-testing.slb.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-testing.slb.maps.yandex.net/show/) |
| Продакшен внутренняя сеть | [front-specprojects-int.slb.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-specprojects-int.slb.maps.yandex.net/show/) |
| Продакшен внешняя сеть | [front-specprojects-ext.slb.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-specprojects-ext.slb.maps.yandex.net/show/) |
## Новым разработчикам

Для локальной работы с любым проектом нужно, чтобы у вас были прописаны необходимые переменные окружения. Например, в `~/.bashrc`

#### 1. `NODE_EXTRA_CA_CERTS`
Исправляет ошибку самоподписного сертификата `error: self signed certificate in certificate chain`.

Скачайте YandexInternalRootCA:
```
sudo wget https://crls.yandex.net/YandexInternalRootCA.crt -O /etc/ssl/certs/YandexInternalRootCA.crt
```
Добавьте путь к сертификату в переменную окружения:
```
NODE_EXTRA_CA_CERTS /etc/ssl/certs/YandexInternalRootCA.crt
```

#### Самоподписанный сертификат в браузере
Если браузер ругается на недостоверный сертификат на MacOS, нужно:
- в корне проекта выполнить `make local`
- открыть папку, в которой лежит сгенерированный сертиифкат, дважды кликнуть по нему
- в ключнице найти этот сертификат и изменить параметры доверия на `всегда доверять`
Этот способ сработает для ябро.

#### 2. `STATIC_CLIENT_KEY`
Позволяет выкладывать статику на S3 при сборке. Секрет [тут](https://yav.yandex-team.ru/secret/sec-01cjz2vkw9hqhf3c7skw5g4zxt).

#### 3. `QTOOLS_TOKEN`
Нужен для корректной работы qtools и релиза приложений. Секрет [тут](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=4dd38b9acbb44ad8a7ece163ddf1c53a).


## Тесты
### Запуск
Для локального запуска тестов из директории проекта выполните `make test`.
Чтобы запусить отдельно тесты для сервера и отдельно - для клиента, выполните `make test-client` или `make test-server`

### Написание тестов
Покрываем тестами важные сценарии. Тесты пишем на `typescript`. Файлы с тестами лежат в тех же директориях, что и тестируемый код. В названии файла используем суффикс `.spec.ts`. Проверяемые сценарии пишем на русском языке.

### Релиз
Процедура релиза:

1) Посмотрите в гите текущую версию приложения (последний закоммиченный тег определенного спецпроекта).
2) Решите, какое будет следующее обновление: `patch/minor/major`.
3) Отведите релизную ветку от `master` с именем `release-<номер будущей ветки из шага 2>`. Запушьте эту ветку в гит.
4) В релизную ветку влейте изменения из веток, которые вы хотите выкатить в продакшен.
5) В релизной ветке:
   - `make patch/minor/major` (в зависимости от решения в п.2) - поднять версию
   - `git push --follow-tags` - запушить изменения в гит
   - дождитесь успешного прогона тестов в релизной ветке (прогресс можно посмотреть в гите)
   - опционально: выкатите релизную ветку в тестинг окружение и пройдите ручное тестирование
   - сделайте пул-реквест из релизной ветки в `master`, еще раз проверьте глазами дифф
   - влейте релизную ветку в master
6) Загрузите свежие изменения из ветки `master`: `git checkout master && git pull origin master`
7) Из ветки `master`:
   - `make release-testing` - выкатить в тестинг новую версию
   - `make deploy-production` - задеплоить изменения в продакшен


## Регулярный запуск задач
Скрипты создаются в поддиректории проекта, например `projects/my_project/scripts/sandbox`, со своим собственным `package.json`.
В файле `.tvm.json` секреты берем из переменных окружения. Пример: `env:MY_SECRET`.
Принцип работы:
- В Sandbox создаем планировщик который периодически запускает задачу.
- Задача скачивает репозиторий.
- Переходит в директорию скрипта.
- Устанавливает необходимые зависимости.
- В фоне запускает tvm-демон.
- Запускает скрипт.
- Убивает tvm-демон.
### Настраиваем планировщик в sandbox.yandex-team.ru:
1. Создаем планировщик (Create -> Scheduler).
2. В поле `Enter scheduler type` указываем `TRENDBOX_CI_JOB`.
3. В `Owner` указываем Sandbox-группу которая синхронизирована с ABC-группой. Если такой группы нет, ее нужно создать (Create -> Group).
4. В поле `Job configuration` указываем json для конфигурации tandbox.
Пример:
```
{
    "debugShell": true,
    "language": "node_js",
    "env": {
        "node_js": 10
    },
    "lifecycle": {
        "prepare": [
            "trendbox checkout -c $checkout_config --dir sources",
            "cd sources; hash -r",
            "curl https://crls.yandex.net/YandexInternalRootCA.crt -o $PWD/YandexInternalRootCA.crt",
            "export NODE_EXTRA_CA_CERTS=$PWD/YandexInternalRootCA.crt"
        ],
        "install": [
            "nvm install $node_js",
            "cd ./projects/ingrad/scripts/sandbox",
            "npm ci"
        ],
        "before_script": "node_modules/.bin/tvmtool --port 8081 --auth tvmtool-development-access-token >/dev/null 2>&1 &",
        "script": "node_modules/.bin/ts-node ./crm/send-leads.ts",
        "after_script": "kill %1"
    },
    "checkout": {
        "type": "git",
        "url": "https://github.yandex-team.ru/maps/specprojects.git",
        "branch": "master"
    }
}
```
5. Можно настроить частоту запуска и уведомления при ошибках.
6. Sandbox пользуется своими отдельными секретами (Create -> Valult).
Vault должен иметь в названии префикс `env.`, тогда секрет будет доступным из переменной окружения. Пример: `env.MY_SECRET`. В `Ovner` указывать Sandbox-группу.
