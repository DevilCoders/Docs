# Как начать поднимать renderer-беты с шаблонами вашего сервиса

_Общая информация про беты находится [здесь](./general.md)._

Подразумевается, что беты рендерер вы захотитие запускать только если вы используете/планируете использовать рендерер в продакшене. Для обоих контекстов существует ряд общих предусловий. Необходимые шаги для подъема рендерера с шаблонами в продакшене можно посмотреть в [отдельной документации](https://a.yandex-team.ru/arc_vcs/frontend/docs/how-to/deploy-rr-templates-to-production.md?rev=r7569855).

## Предусловия

#### 1. Иметь report-renderer-совместимые шаблоны

[API шаблонов](https://wiki.yandex-team.ru/search-interfaces/infra/report-renderer/templates-api/#shablonyikonfiguracionnyefajjly). На примере ydo:

- [Шаблон](https://a.yandex-team.ru/arc_vcs/frontend/services/ydo/src/report-renderer/index.ts?rev=r8049832#L28)
- [Конфигурация шаблона](https://a.yandex-team.ru/arc_vcs/frontend/services/ydo/.config/renderer/desktop.json?rev=r8049832)
- [Конфигурация пакета шаблонов](https://a.yandex-team.ru/arc_vcs/frontend/services/ydo/routes.json?rev=r6330848)

#### 2. Уметь собирать архивы с шаблонами

Это потребуется для публикации бета-версии шаблонов в sandbox-ресурс. Для сборки таких архивов обычно используют [tartifacts](https://github.com/yandex/tartifacts).

[Пример tartifacts-конфига ydo](https://a.yandex-team.ru/arc_vcs/frontend/services/ydo/.config/tartifacts/dynamic.js?rev=r7542900). Также здесь могут потребоваться некоторые предварительные шаги, например, сборка webpack'ом, которые соответственно тоже должны быть реализованы. Необходимые для генерации архива команды следует зафиксировать в npm-скрипте в `package.json`.

#### 3. Иметь тип ресурса в sandbox для архива с шаблонами

Для возможности публикации собранных шаблонов в sandbox-ресурсы необходимо предварительно завести новый тип ресурса. Здесь есть 2 варианта:

- добавляем вручную новый класс ресурса в [файл](https://a.yandex-team.ru/arc_vcs/sandbox/projects/sandbox_ci/resources/template_packages.py?rev=r7911611) с указанием списка логинов, которым разрешается релизить ресурсы создаваемого типа, например:

```python
class WebDocDemoMicroPackage(ReportWebTemplatesPackage):
    releasers = ['some-login-1', 'some-login-2'] + ROBOTS + INFRA_TEAM
```

Имя класса определяет тип ресурса. Для приведенного примера будет заведен тип `WEB_DOC_DEMO_MICRO_PACKAGE`. В [обычных случаях](https://a.yandex-team.ru/arc_vcs/frontend/docs/faq/release-workflow.md?rev=r8156369#%D0%B2%D1%8B%D0%BA%D0%BB%D0%B0%D0%B4%D0%BA%D0%B0-%D0%B2-%D0%BF%D1%80%D0%BE%D0%B4%D0%B0%D0%BA%D1%88%D0%B5%D0%BD) для выкладки релиза не требуется указывать кастомных releasers, поскольку по умолчанию для этого используются роботы. Если такое умолчание вас устраивает, тело класса ресурса можно не переопределять, указав ключевое слово `pass`.

- если ваш сервис основан на [стабе из монорепы](https://a.yandex-team.ru/arc_vcs/frontend/services/stub?rev=r8120213) или просто использует пакет [apphost-service](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/apphost-service?rev=r8115529), можно воспользоваться командой [`update-package`](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/apphost-service?rev=r8115529#update-package) пакета, указывая такое же название класса, как и для ручного добавления, и, при необходимости, список релизеров.

## Деплой бет

#### 4. Определиться с квотой, под которой ваши беты будут запускаться

Подробнее о квотах можно почитать на [соседней страничке](./quotas.md). Вкратце, если для ваших бет не требуется кастомизаций окружения и не ожидается более 10-15 одновременно открытых и активных пулл-реквестов, и вы заезжаете в монорепу [frontend](https://a.yandex-team.ru/arc_vcs/frontend), вам подойдет общая квота монорепы - `report-renderer-templates`.

Причина, по которой сейчас не следует использовать общую квоту в отдельных репозиториях - [несовершенство](https://a.yandex-team.ru/arc_vcs/frontend) текущей реализации шедулера очистки старых бет. Если вы захотите использовать общую квоту в отдельной репе - можно прийти в infraduty, вероятно, будем улучшать шедулер.

#### 5. Определить список имен источников для подмены

Рендерер работает под аппхостом, соответственно у вас должен иметься граф, в котором будут определены и вершины с рендерером. Определяем список имен вершин, для которых хотим подменять указанные в графе бекенды на бекенды рендерера с бета-версией шаблонов. Также необходимо понять, требуются ли для запросов в эти графы какие-либо специфичные cgi-параметры и заголовки.

Например, в графе [jobs](https://a.yandex-team.ru/arc_vcs/apphost/conf/verticals/JOBS/jobs.json) вершинами с рендерером являются `ROUTER`, `TEMPLATES` и `CUSTOM_RESPONSE`.

#### 6. Завести конфиг для бет

Создаем конфиг для бет вашего сервиса, указывая выбранную квоту, подменяемые источники, кастомные cgi-параметры при необходимости, и задавая идентификатор шаблона, который определяет префикс урлов, по которым будут доступны поднимаемые беты. Следует указывать `id`, начинающийся с `renderer-`.

Пример конфигурации:
```json
{
    "id": "renderer-doc-demo",
    "quota": "report-renderer-templates",
    "auth": {
        "groups": [1492]
    },
    "component": {
        "timeout": 5000,
        "sourceNames": ["TEMPLATES", "DOC_DEMO_TEMPLATES", "RENDERER", "RENDERER_DEMO"]
    },
    "ttl": 96
}
```
Подробнее о доступных опциях конфигурации можно почитать в документации утилиты [`renderer-betas-cli`](./renderer-betas-cli.html#format-konfiguratsii).

Больше примеров конфигурации можно посмотреть в коде существующих сервисов, например, [ydo](https://a.yandex-team.ru/arc_vcs/frontend/services/ydo/.config/renderer-betas/config.json?rev=r7308165), где можно увидеть кастомизацию cgi-параметров.

#### 7. Завести скрипты деплоя/остановки бет

_Альтернативной явного заведения скриптов может быть использование пакета [frontend.ci.deploy](#frontend-ci-deploy)._

Далее необходимо описать непосредственно команды запуска и остановки бет с использованием соответствующих команд [`renderer-betas-cli`](./renderer-betas-cli.html#komandy-i-optsii). Удобно их будет описать в отдельных файлах. Важно заметить, что к моменту вызова команды [create](./renderer-betas-cli.html#komandy-i-optsii) ресурс с бета-версией шаблонов уже должен быть опубликован в сендбокс, и мы должны иметь его идентификатор. Эти действия могут быть произведены в этом же или соседнем скрипте.

Примеры базовых скриптов [деплоя](https://a.yandex-team.ru/arc_vcs/frontend/services/ydo-admin/tools/deploy-dynamic.js?rev=r7316552) и [остановки](https://a.yandex-team.ru/arc_vcs/frontend/services/ydo-admin/tools/deploy-remove.sh?rev=r8173946) бет из ydo.

Здесь же возможны дополнительные кастомизации для ваших бет, например в [скрипте деплоя бет jobs](https://a.yandex-team.ru/arc_vcs/frontend/services/jobs/tools/deploy-dynamic.js?rev=r8078492#L39) помимо обязательных параметров также передаются кастомные заголовки, которые будут добавляться к каждому запросу при обращении по виртуальному домену (урлу) беты.

#### 8. Подключить заведенные скрипты к CI

_В случае использования [frontend.ci.deploy](#frontend-ci-deploy) скрипты заменяются на команды утилиты._

В монорепе frontend сервисы могут определить в `package.json` скрипты с [предопределенными именами](https://a.yandex-team.ru/arc_vcs/frontend/docs/faq/checks.md?rev=r8040410#%D1%81%D0%BF%D0%B8%D1%81%D0%BE%D0%BA-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D0%B0%D0%B5%D0%BC%D1%8B%D1%85-%D0%B2-ci-%D1%81%D0%BA%D1%80%D0%B8%D0%BF%D1%82%D0%BE%D0%B2), которые будут поднимать беты в [определенный момент](https://a.yandex-team.ru/arc_vcs/frontend/docs/faq/checks.md?rev=r8040410#события-запуска-cideploy-скриптов). На примере ydo-admin - [скрипт деплоя бет в пулл-реквестах](https://a.yandex-team.ru/arc_vcs/frontend/services/ydo-admin/package.json?rev=r8176155#L33) и вся цепочка дальнейших вызовов в scripts.

#### 9. Заказать дырки до сетевых макросов ваших бет

Может потребоваться заказать дырки до сетевого макроса с вашими бетами, например, из сетевого макроса вашего аппхоста или других макросов, в зависимости от инсталляции. Для бет в общей квоте фронтенда макрос носит имя `_RENDERER_FRONTEND_BETAS_NETS_`. Если для вас была заведена кастомная квота, то для ваших бет будет заведен новый макрос. Заказывать следует следующие tcp диапазоны: `4000-4400`, `80-400`, `800-1200`. Пример запроса - [DOSTUPREQ-215555](https://st.yandex-team.ru/DOSTUPREQ-215555).

Список соответствия сетевых макросов для всех квот:

| yappy-квота | сетевой макрос |
| --- | --- |
| `report-renderer-templates` | `_RENDERER_FRONTEND_BETAS_NETS_` |
| `report-renderer-serp` | `_RENDERER_SERP_BETAS_NETS_` |
| `report-renderer-fiji` | `_RENDERER_FIJI_BETAS_NETS_` |
| `report-renderer-turbo` | `_RENDERER_TURBO_BETAS_NETS_` |
| `report-renderer-pcode-common` | `_RENDERER_PCODE_BETAS_NETS_` |
| `report-renderer-chat` | `_RENDERER_CHAT_BETAS_NETS_` |
| `report-renderer-nerpa` | `_RENDERER_NERPA_BETAS_NETS_` |

## frontend.ci.deploy

Как альтернатива для прямого использования `renderer-betas-cli` в монорепе frontend существует инструмент [`frontend.ci.deploy`](https://a.yandex-team.ru/arc_vcs/frontend/packages/frontend.ci.deploy), который служит для унификации деплоя бет (не только renderer), и, в частности, оборачивает `renderer-betas-cli`. `frontend.ci.deploy` имеет свой конфиг, часть из которого под ключом `rendererBetasCliConfig` полностью совпадает с конфигурацией для `renderer-betas-cli`. [Пример конфига для `frontend.ci.deploy` сервиса jobs](https://a.yandex-team.ru/arc_vcs/frontend/services/jobs/.config/deploy/config.json?rev=r8078492).

`frontend.ci.deploy` позволяет упростить часть шагов и для общего случая не требуется заводить отдельные скрипты деплоя/остановки и берет на себя задачу публикации ресурса в sandbox, но в то же время, на данный момент, библиотека не поддерживает более кастомные кейсы, когда при деплое нужно указать дополнительные опции командам утилиты `renderer-betas-cli`, например, `--header`. Выглядит, что лучшим путем будет расширить возможности этой утилиты, чем заводить отдельные скрипты для кастомных случаев.

Команда renderer-betas не занимается разработкой и поддержкой данного пакета и за консультациями по нему следует обращаться к [овнерам](https://a.yandex-team.ru/arc_vcs/frontend/packages/frontend.ci.deploy#owners).
