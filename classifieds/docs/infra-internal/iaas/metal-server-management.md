# Управление серверами

Способы и инструменты управления серверами отличается в зависимости от того, где они живут.

Виртуальные сервера - это:
* сервера в `qyp.yandex-team.ru`;
* lxc-контейнеры, которые налиты на lxc-боксах;
* сервера в Яндекс.Облаке.

Помимо виртуальных серверов, есть и железные сервера, физически расположенные в одном из датацентров.

## Виртуальные сервера

Наливка и управление виртуальными серверами очень просты, и зависят от типа виртуального сервера.

### Виртуальные сервера в qyp

Их наливка выполняется с помощью [qyp-mngr.sh](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-utils/qyp-mngr.sh). Полный перечень принимаемых скриптом параметров можно узнать с помощью команды `./qyp-mngr.sh --help`.

Ниже приведен пример команды для создания виртуальной машины:
```
./qyp-mngr.sh create -p=eljusto-01-dev -c=4 -m=8 -d=100 -g=vertis_vdev_personal -o=eljusto
```

После выполнения скрипта достаточно прогнать в ручном режиме кластерную ansible-плейбуку для данного хоста или проверить, что ansible-pull сделал это без ошибок (при условии, что данный кластер подключен к ansible-pull).

### Lxc-контейнеры

Наливка lxc-контейнеров выполняется с помощью [lxc-mngr.sh](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-utils/lxc-mngr.sh). Полный перечень принимаемых скриптом параметров можно узнать с помощью команды `./lxc-mngr.sh --help`.

Далее, аналогично qyp-серверам, в базовом случае достаточно только прогона плейбуки.

### Сервера в Яндекс.Облаке

Все сервера в Яндекс.Облаке мы конфигурируем с помощью [terraform](https://bb.yandex-team.ru/projects/YANDEX-CLASSIFIEDS/repos/terraform/browse).

Нашу документацию по работе с terraform можно найти [тут](terraform.md). Рекомендуем также ознакомиться с [Best Practices](cloud.md) для Яндекс.Облака.

## Железные сервера

Для переименования хостов мы используем заявки через бота [bot.yandex-team.ru](https://bot.yandex-team.ru/adm/). C помощью бота также можно проводить преднастройку хоста (вводим fqdn -> `поискать` -> выбираем необходимые хосты -> `преднастроить`).

В случае, если с хостом что-то не так, или необходимо произвести апгрейд оборудования (например, заменить диски) - мы работаем с инженерами датацентров через тикет в очередь [ITDC](https://st.yandex-team.ru/createTicket?queue=ITDC).

### Железные docker-сервера

Железными docker-серверами мы управляем через [wall-e.yandex-team.ru](https://wall-e.yandex-team.ru/projects/hosts). Wall-e предоставляет возможность автопочинки хостов и их простую и быструю наливку в автоматическом режиме.

На данный момент Wall-e следит за базовыми проверками на хостах (Полный список проверок можно посмотреть, например, [тут](https://wall-e.yandex-team.ru/host/docker-18-sas.test.vertis.yandex.net/health))
И по определенным инструкциям меняет [статус хоста](https://wiki.yandex-team.ru/wall-e/guide/#host-statuses)

* [Официальная документация Wall-e](https://wiki.yandex-team.ru/wall-e/guide/)
* [Наш проект для тестинга](https://wall-e.yandex-team.ru/project/vertis-docker-test)
* [Наш проект для  прода](https://wall-e.yandex-team.ru/projects/hosts?project=vertis-docker-prod)

#### Инструкция для добавления новых машин в проект

**Перед наливкой хосты для докера необходимо добавить в группу %vertis_test_docker_vlan688 или %vertis_prod_docker_vlan688 (в зависимости от окружения), нужно для правильной настройки сети.**

Для того, чтобы Wall-e начал следить за хостом, его необходимо добавить в проект. Лучше всего это сделать через консольный клиент. [Инструкция по установке](https://wiki.yandex-team.ru/wall-e/guide/#cli).

Пример добавления хоста в проект: `wall-e hosts add vertis-docker-test docker-03-myt.test.vertis.yandex.net`

Далее можно ждать пока он переналется автоматикой или сделать это руками:

{% cut "Инструкция" %}

1. Открываем Web-интерфейс
    ![image](images/wall-e-project.png)

2. Отмечаем галочкой машины, которые необходимо переналить, и нажимаем кнопку `Redeploy`.
    ![image](images/redeploy-hosts.png)

3. В появившемся окне можно поставить галку напротив `Ignore CMS`, если переналиваем более двух машин. В противном случае машины будут наливаться по 2 (ограничение нашего проекта - операции над машинами разрешены не более, чем на двух хостах одновременно).
    ![image](images/redeploy-host-card.png)

{% endcut %}

Как только хост будет налит, на него придет Rundeck и принесет на него секрет ([таска](https://rundeck.vertis.yandex.net/project/sandbox/job/show/0635b0c1-7de6-46ce-b94e-37beb8bbd3ae) запускается раз в 15 минут). Всю дальнейшую работу сделает ansible-pull.

#### Как удалить хост в Wall-e

В Web UI находим нужный хост, открываем выпадающее меню и жмем `Remove`.

{% cut "Инструкция" %}

![image](images/remove-host.png)

{% endcut %}

### Остальные железные сервера

Наливка остальных железных серверов, которые не относятся к docker-кластеру, проводится с помощью скрипта [project_id_nalivka.sh](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-utils/project_id_nalivka.sh).

Пример использования скрипта:
```
./project_id_nalivka.sh -с vertis-l3-prod-xfs-ubuntu-16.04 -h php-16-myt.prod.vertis.yandex.net -s
-c конфиг наливки из setup. Параметр необязательный. По умолчанию используется конфиг vertis-l3-(prod|test)-xfs-ubuntu-16.04.
-s не переводить хост в project_id а просто налить. Данный параметр тоже необязательный.
```

#### Логика работы project_id_nalivka.sh

1. По имени хоста определяется `env` (тестинг или прод).
2. Добавляется downtime на хост продолжительностью 2 часа. Если это lxcbox - ставится даунтайм для всех дочерних контейнеров.
3. Определяется свич и порт в eine.
    * Если невозможно определить свич и порт (встречается достаточно часто для серверов в Сасово), сервер переводится в кондукторную группу `vertis_parking` и [eine](https://eine.yandex-team.ru/) запускает для него профиль `discovery`.
    * Если свич и порт успешно определился, меняем vlan на `VERTISDEVNETS` или же на `VERTISPRODNETS` на основе `env` из первого пункта.
4. Затем выполняется установка ОС через обертку над [yasetup](https://wiki.yandex-team.ru/dca/services/setup/user/client/) - [vertis-yasetup.sh](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-utils/vertis-yasetup.sh).
5. Далее нужно выбрать удалять ли из DNS запись о хосте, лучше всего это делать при переезде в `project_id`. При обычной переналивке DNS записи удалять не нужно, так как это может сломать nginx. Для lxcbox DNS записи для всех контейнеров удаляются в любом случае.

** Что нужно для работы project_id_nalivka.sh**:

Переменная окружения `$YAV_OAUTH_TOKEN` - Требуется для похода в секретницу, подробнее можно прочитать [тут](https://vault-api.passport.yandex.net/docs/);

Консольная версия `yasetup` для наливки хоста, подробнее можно прочитать [тут](https://wiki.yandex-team.ru/dca/services/setup/for-customers/client/?from=%252Fhaas%252Fservices%252Fsetup%252Fclient%252F);

Переменная окружения `$JUGGLER_OAUTH_TOKEN` - подробнее можно взять [тут](https://juggler.yandex-team.ru/) (правый нижний угол);

Переменная окружения `$CONDUCTOR_OAUTH_TOKEN` - подробнее можно прочитать [тут](https://wiki.yandex-team.ru/conductor/api/).

{% cut "Работа vertis-yasetup.sh" %}

Под капотом у `project_id_nalivka.sh` лежит скрипт `vertis-yasetup.sh`.

Задача `vertis-yasetup.sh` просто налить тачку без перевода в `project_id`, удаления dns записей (то же самое, если запустить `project_id_nalivka.sh` с опцией `-s`).

Пример использования `vertis-yasetup.sh`:
```
./vertis-yasetup.sh -с config_from_setup -h hostname
```

Логика работы `vertis-yasetup.sh` следующая:

1. Получает актуальную версию первичного ssh-ключа из секретницы;
2. Используя версию, скрипт получает ключ и кладет его в /tmp/;
3. Затем запускает yasetup с ключом -p который служит для передачи приватных данных. Подробнее можно прочитать [тут](https://wiki.yandex-team.ru/dca/services/setup/for-customers/client/#otpravkaprivatnyxdannyx);
4. Если один из шагов фейлится, секрет удаляется из /tmp/.

{% endcut %}

#### Частные проблемы при работе с project_id_nalivka.sh

1. Скрипт `project_id_nalivka.sh` отрабатывает успешно, но сервер перезагружается в старую ОС. Нужно проверить наличие ipxe, так как intel boot manager не умеет ipv6. Если нет ipxe, то запустить common-firmware профиль в [eine](https://eine.yandex-team.ru/).
2. Если после наливки не отрабатывает playbook, нужно проверить наличие /root/.ssh/id_rsa_datasources. Если его нет, тогда запустить кластерную плейбуку руками.
3. Если фейлится предыдущий шаг и машинка не новая, то скорее всего проблема в том, что нужно удалить старый хост из /.ssh/known_hosts: `ssh-keygen -R <hostname>`
