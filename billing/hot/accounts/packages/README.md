## Выкладка и CI
Настроен аркадийный CI для всех компонентов: https://a.yandex-team.ru/projects/newbillingaccountupdater/ci/releases/timeline.
Для каждого deploy unit'а (api, aggregates, lbexport, tasks) описан свой релиз.
Запускается очевидной жёлтой кнопочкой в интерфейсе CI'я, после выкладки в тест нужно ручное подтверждение в графе релиза.
Так же нужно дополнительное подтверждение на выкладку в интерфейсе deploy'я в разделе [Deploy Tickets](https://deploy.yandex-team.ru/stages/billing-accounts-prod-stage/deploy-tickets).

Ключевая особенность выкладки через CI - она умеет обновлять только docker-образы, а на данный момент конфиги подключены
отдельными статическими ресурсами и потому их выложить можно только вручную, через [консоль](https://deploy.yandex-team.ru/docs/tools/dctl) или UI.
Для этого:
1. Загружаем куда-нибудь конфигурационные файлы:
   * Конфиг приложения из соответствующей папки `ya upload configs/api/dev.yaml --mds --ttl 100`
   * Настройки плана счетов `ya upload configs/settings/dev.yaml --mds --ttl 100`
2. Правим настройки в UI: https://deploy.yandex-team.ru/stages/billing-accounts-test-stage/edit/du-api/box-billing-accounts-api
    * Конфиг приложения - `Additional Layers - Static Resources`, меняем ссылку в первом блоке, в котором путь `/config`
    * Настройки - `Additional Layers - Static Resources`, меняем ссылку в первом блоке, в котором путь `/settings`
3. Жмём `Update`

Если важно атомарно выкатить версию приложения и конфиги то нужно каким-либо образом собрать докер-образ [см. ниже](#manual-build) и вместе с конфигами указать новую версию пакета в разделе `Base Layer`.

## Настройка и разворачивание компонента в ЯДеплое
### Ссылки
* Инструкция https://wiki.yandex-team.ru/balance/billing30/deployinstruction/
* Проект в деплое https://deploy.yandex-team.ru/projects/billing-accounts
* Топики для логов в логброкере
  https://logbroker.yandex-team.ru/logbroker/accounts/billing-accounts/accounts/test
  https://logbroker.yandex-team.ru/logbroker/accounts/billing-accounts/accounts/prod
* todo-igogor логи в YT

### Как подготовить отдельную часть приложения для выкладки в деплой
1. Добавляем папку в `billing/hot/accounts/packages`

1. Добавляем скрипт запуска с именем `run.sh`
1. Добавляем в ней Dockerfile.
   Он должен скопировать в себя нужный бинарь и скрипт запуска.
   При этом точкой входа Dockerfile должен быть скрипт `run-predeploy.sh` а не `run.sh`.
   Причина описана в разделе как запускается приложение.

1. Пишем `pkg.json`. Он он нужен чтобы собирать докер образ через ya package и в сэндбоксе.
1. Собираем докер, смотрим что без ошибок
   ```ya package --docker-repository balance --docker packages/tasks/pkg.json```.

   Отправляем докер в репозиторий
   ```ya package --docker-repository balance --docker packages/tasks/pkg.json --docker-push```

   todo-igogor все сервисы горячего биллинга льются в balance, это не оч правильно т.к. есть billing

1. Для сборки в сэндбоксе к образу нужны доступы роботу `robot-billing-ci` а для доступа из деплоя `robot-qloud-client`.
   Но выдавать им ничего не надо, т.к. им уже даны доступы на префикс `balance`

1. Для удобства команды сборки и аплоада образа добавляем в Makefile

### Как добавить в деплой
По инструкции Игоря Андреева https://wiki.yandex-team.ru/balance/billing30/deployinstruction/#3.sozdaemproektvdeploy

Примечания
* В качестве `Start command` для ворклоада надо указывать `/run-predeploy.sh`, а не `run.sh`.
  Иначе логи литься в логброкер не будут.

* Конфиги пока заливаем в mds через `ya upload` и добавляем как статический ресурс в настройках Box'a.
* Пути конфигов и секретов передаем через переменные окружения workload'a.

### Как запускается приложение
1. В деплое в качестве команды запуска по инструкции указываем запуск скрипта `/run-predeploy.sh`
  Это скрипт из базового образа. Он запускает supervisor.

2. В supervisor в базовом образе добавлен конфиг для запуска приложения `/etc/supervisor/conf.d/app.conf`

3. По этому конфигу supervisor запускает скрипт из базового образа `/run-wrapper.sh`
4. Который в свою очередь запускает скрипт `/run.sh`.
   Этот скрипт кастомный - его должны предоставить мы. Он должен содержать команду запуска приложения.
   Пока докер мы используем чтобы доставить бинарь и этот файл с командой запуска.

### Где лежат логи приложения в box'e
`less /var/log/supervisor/app.log`

Из этого же файла клиент логброкера считывает изменения

### <a name="manual-build"/> Как собрать докер образ
1. Вручную
    * В Makefile добавлены команды для билда и пуша докер образов.
      Например `make docker-image-tasks-push`.
    * Если хотим кастомную версию, то
      `make docker-image-tasks-push -- --custom-version svn.7839077-sandbox.0.1`.
    * Не забываем проверять что версия не занята
      `curl -H "Authorization: OAuth AQAD-..." -v https://registry.yandex.net/v2/balance/yb-hot-accounts-tasks/tags/list`
    * Помним, что нужна авторизация https://wiki.yandex-team.ru/qloud/docker-registry/#authorization
      и право на аплоад докера https://idm.yandex-team.ru/system/docker#role=29702298,f-role-id=29702298

2. Через сэндбокс

   Пример сборки: https://sandbox.yandex-team.ru/task/892829092/view

