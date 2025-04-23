# drills-helper

Cli-тулза для управления учениями в Вертикалях. Сейчас умеет:
* [Открывать и закрывать](https://docs.yandex-team.ru/classifieds-ops-internal/duty/drills-helper#upravlenie-load-balancers) балансировщики нагрузки
* [Переключать мастеров](https://docs.yandex-team.ru/classifieds-ops-internal/duty/drills-helper#pereklyuchenie-masterov) teamcity , jenkins , rundeck
* [Выключать/Включать](https://docs.yandex-team.ru/classifieds-ops-internal/duty/drills-helper#om) vmagent
* [Включать/Выключать](https://docs.yandex-team.ru/classifieds-ops-internal/duty/drills-helper#upravlenie-hbf) режим HBF
* Проставлять аннотации на все действия выше
* [Выключать деплой](https://docs.yandex-team.ru/classifieds-ops-internal/duty/drills-helper#upravlenie-deploem) в shiva , conductor , jenkins
* [Управлять автопочинкой](https://docs.yandex-team.ru/classifieds-ops-internal/duty/drills-helper#upravlenie-avtopochinkoj-wall-e) Wall-e
* [Проставлять даунтайм](https://docs.yandex-team.ru/classifieds-ops-internal/duty/drills-helper#prostavlenie-dauntajma-v-dzhaglere-na-vesь-data-centr) в Джаглере на дата-центр

## Установка
```Актуальная версия 1.11```

### Установка и обновление для macOS:
```
brew tap YandexClassifieds/vertis ssh://git@bb.yandex-team.ru/yandex-classifieds/homebrew-vertis.git
brew update
brew install drills-helper

Обновиться до последней версии:

brew update
brew upgrade yandexclassifieds/vertis/drills-helper
```

### Установка для Linux:
```
sudo curl https://proxy.sandbox.yandex-team.ru/2746798738 -o /usr/local/bin/drills-helper && sudo chmod +x /usr/local/bin/drills-helper
```

### Секреты
Для работы кли, а также для запуска тестов необходимы некоторые секреты (OAuth токены и т.д.)

Для обычной работы их нужно положить в переменные окружения.

Для запуска тестов их стоит положить в local.env  в корне проекта (подробнее - см. README)

{% cut "DH_OAUTH_TOKEN" %}

Токен можно взять по ссылке: <https://oauth.yandex-team.ru/authorize?response_type=token&client_id=cd3fb5f8e5e141daa50a5de91ea88194>

{% endcut %}


{% cut "GRAFANA_TOKEN" %}

Токен можно взять здесь - <https://yav.yandex-team.ru/secret/sec-01eyqxkth9tkf8ak76y7h4y4z7>

{% endcut %}

{% cut "JENKINS_USER, JENKINS_PASSWORD" %}

1. Заходим <https://j.vertis.yandex-team.ru/>
2. Заходим в своего пользователя
![картинка](images/my-user.png)
3. Переходим в настройки
![картинка](images/configure-jenkins.png)
4. Токен!
![картинка](images/jenkins-token.png)

{% endcut %}

Также понадобится добавить основной SSH ключ в SSH агента (это необходимо для хождения по ссш на хосты):
`ssh-add <path-to-your-key>`

## Использование

### Управление деплоем
Есть две команды - `deploy enable`  и `deploy disable` , соотв. включающие и отключающие деплои.
Каждая из них принимает один позиционный аргумент - систему деплоя:
* `conductor`
* `shiva`
* `jenkins`
* `all`  (композитный макрос для всех систем выше, при его указании будут последовательно включены/выключены деплои во всех поддерживаемых системах)

Также, эти команды требуют указания двух обязательных флагов - датацентр (`sas/vla`), в котором отключать деплой, а также окружение (`test/prod`).

### Примеры
* Выключить **все** деплои в **проде** в **Сасово**:

    `drills-helper deploy disable all -l prod -d sas`
* Включить **все** деплои в **проде** в **Сасово**:

    `drills-helper deploy enable all -l prod -d sas`
* Выключить деплой в **Шиве** в **тестинге** во **Владимире**:

    `drills-helper deploy disable shiva -l test -d vla`
* Включить деплой в **Дженкинсе** в **проде** во **Владимире**:

    `drills-helper deploy enable jenkins -l prod -d vla`

## Переключение мастеров
Команда `switch`.

Принимает один обязательный позиционный аргумент - какой сервис переключить:
* `teamcity`
* `jenkins`
* `rundeck`
* `all`  (композитный макрос для всех сервисов выше, при его указании будут последовательно переключены мастера во всех поддерживаемых сервисах)

Также требует указания из какого датацентра переключить мастера. Если в указанном дц мастера нет - выведется предупреждение.

### Примеры
* Переключить мастер **teamcity** из **Сасово**:

    `drills-helper switch teamcity --from sas`
* Переключить всех поддерживаемых мастеров из **Владимира**:

    `drills-helper switch all --from vla`

## Проставление даунтайма в Джаглере на весь дата-центр
Команда `downtime`

Команда `dt`

Принимает один обязательный позиционный аргумент - насколько времени поставить даунтайм (считая от текущего момента времени):
Требует указания двух обязательных флагов - датацентр (`sas/vla/man`), на который поставить даунтайм, а также окружение (`test/prod`)

### Примеры
* Поставить даунтайм на 2 часа в **Сасово** в **проде**:

    `drills-helper dt 2h -d sas -l prod`

## Управление `vmagent`-ом
Две команды - `vmagent stop` и `vmagent start`

Принимает один обязательный флаг - датацентр (`sas/vla`)

### Примеры
* Выключить `vmagent` в **Сасово**:
    `drills-helper vmagent stop -d sas`
* Включить `vmagent` во **Владимире**:
    `drills-helper vmagent start -d vla`

## Управление load balancers
Две команды - `lb close` и `lb open`, соотвественно закрывающая и открывающая балансеры.

Каждая из них принимает один позиционный аргумент - балансер:
* `ingress `
* `upstream `
* `lb-int `
* `lb-int-nginx `

Требует указания обязательного флага - датацентр (`sas|vla`). Работает только для прода.

### Примеры
* Закрыться от внешнего трафика в **Сасово**:
    `drills-helper lb close ingress -d sas`
* Открыть для трафика lb-int c envoy во **Владимире**:
    `drills-helper lb open lb-int -d vla`

## Управление автопочинкой Wall-e
Две команды - `walle disable` и `walle enable`, соотвественно выключающая и включающая автопочинку хостов в Wall-e.
Требует указания обязательного флага - окружение (`test|prod`).

### Примеры
Выключить автопочинку в **Проде**:
    `drills-helper walle disable -l prod`
Включить автопочинку в **Тестинге**:
    `drills-helper walle enable -l test`

## Управление HBF
Две команды - `hbf start` и `hbf stop`, для старта и отмены HBF соответственно.

* `hbf start `

    Принимает 1 позиционный параметр - длительность режима HBF. **Выставляет начало через 5 минут после запуска команды.** Сделано специально, чтобы была возможность отменить учения до их начала.

    Принимает **необязательный** параметр `-i, --issue`, в который можно передать тикет. Он будет прикреплен к HBF учениям в интерфейсе.

Обе команды требуют указания обязательного флага - датацентр (`sas|vla|man|myt`). Работает только для прода.

### Особенности HBF
Мы создаем по пресету на каждый датацентр в интерфейсе Топки - https://firewall.yandex-team.ru/drills. Эти пресеты используются в качестве шаблонов для создания учений (то есть оттуда берутся все параметры, кроме длительности).

Все пресеты создаются и редактируются из-под робота robot-vertis-drills@ ([creds](https://yav.yandex-team.ru/secret/sec-01fe9552b3yr558z89yf60mpqg/explore/versions)).

> Айдишники пресетов захардкожены в дрилс-хелпере, так что следует именно изменять существующие, а не создавать новые.

### Примеры
* Начать HBF в **Сасово** с тикетом:
    `drills-helper hbf start 2h -d sas -i VERTISADMIN-26515`
* Отменить учения во **Владимире**:
    `drills-helper hbf stop -d vla`

## Pipeline
Две команды - `pipeline close` и `pipeline open`, для выполнения действий соотвественно при закрытии и открытии ДЦ.

Для команд добавлены короткие альясы, что позволяет сократить команды до `p c` и `p o` соотвественно.

Требует указания:
* обязательного флага `-d` - датацентр (`sas|vla`);
* обязательного флага `-t` - длительность (`2h|30m|1h15m`);
* необязательного флага `-a` - c ним добавляется выключение shiva деплоя в тестинге для ДЦ и простановка downtime для тестинга. Используется при общеяндексовых учениях или регламентных работах, когда тестинг тоже принимает участие.
* необязательного флага `-i` - тикет на учения. При указании тикета, он будет прикреплен к учениям HBF.

### Примеры
* Запуск pipeline закрытия **Сасово** на 2 часа для вертикальных учений:
    `drills-helper p c -d sas -t 2h`
* Запуск pipeline закрытия **Сасово** на 2 часа для общеяндексовых регламентных работ или учений:
    `drills-helper p c -d sas -t 2h -a`
* Запуск pipeline открытия **Владимира** для вертикальных учений:
    `drills-helper p o -d vla`
* Запуск pipeline открытия **Владимира** для общеяндексовых регламентных работ или учений:
    `drills-helper p o -d vla -a`

## Разработка
Язык: `Go`

Репозиторий: https://a.yandex-team.ru/arc_vcs/classifieds/infra/drills-helper
