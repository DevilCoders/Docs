# Teamcity agents

Краткое описание по агентам Teamcity для фронтовых проектов Travel.

## Настройка новой VM в QYP с агентами Teamcity

### Заведение VM в QYP

1. Name: `travel-front-teamcity-<датацентр>` (пример: `travel-front-teamcity-man`)
2. Network: `_DATAUI_TRAVEL_NETS_`
3. ABC Service(Quota): `Фронтенд Яндекс.Путешествий`
4. Segment: `Default`
5. Base OS: `bionic-dev`
6. Disk: `> 500 GB (SSD)`
7. Disk bandwith: `> 60`
8. Network bandwidth: `0`
9. Internet Access: `NAT64`
10. Groups: `Разработка (Фронтенд Яндекс.Путешествий)`

### Установка и настройка docker

1. Обновляем зависимости: `apt update && apt upgrade -y && apt dist-upgrade -y`
2. Устанавливаем docker по [инструкции](https://docs.docker.com/engine/install/ubuntu/)
3. Проверяем, что docker работает: `sudo docker run hello-world`
4. Разрешаем пользователю teamcity использовать docker: `adduser teamcity docker`
5. Логинимся под пользователем teamcity и аутентифицируемся в docker registry:
    - `su teamcity`
    - `docker login -u $USER -p <YOUR_TOKEN> registry.yandex.net` токен в YAV [docker-oauth-token](https://yav.yandex-team.ru/secret/sec-01d1h99ncsm9h5jemms4s7mthc/explore/versions)
6. Настраиваем доступ в сеть для docker-контейнеров:
    - Записываем в `/etc/docker/daemon.json` содержимое из https://paste.yandex-team.ru/5866859
    - `service docker stop && ip link del docker0 && service docker start`
    - `ip6tables -t nat -A POSTROUTING -o eth0 -j MASQUERADE`
    - `sysctl -w net.ipv6.conf.all.forwarding=1`
    - Раскомментируйте строчку в `net.ipv6.conf.all.forwarding=1` в `/etc/sysctl.conf`
    - `apt install iptables-persistent`
    - `ip6tables -t nat -A POSTROUTING \! -o docker0 -j MASQUERADE`
7. Добавляем необходимые секреты и ключи:
    - Записываем содержимое из `https://paste.yandex-team.ru/5866659` в файл `/home/teamcity/.npmrc`. Токен <NPM_AUTH_TOKEN> в YAV [npm-npmrc-authToken](https://yav.yandex-team.ru/secret/sec-01d1h99ncsm9h5jemms4s7mthc/explore/versions)
    - Записываем содержимое из YAV [ssh-public-key](https://yav.yandex-team.ru/secret/sec-01d1h99ncsm9h5jemms4s7mthc/explore/versions) в файл `/home/teamcity/.ssh/id_rsa` и проставляем на этот ключ права: `chmod 600 /home/teamcity/.ssh/id_rsa`

### Установка пакетов для сборки

1. Устанавливаем Node.js по [инструкции](https://github.com/nodesource/distributions/blob/master/README.md):
    - Скрипт для скачивания версии 12.x https://paste.yandex-team.ru/5866842
    - Установка: `sudo apt-get install -y nodejs`
2. Пакетик для инициации деплоя в qloud: `npm install -g --registry="npm.yandex-team.ru" @yandex-data-ui/platform-tools`
3. Пакетик ya tool: https://wiki.yandex-team.ru/yatool/distrib/
4. Разное: `apt install -y build-essential python3-distutils python3-requests zip libdrm2 libgbm1 libxshmfence1 jq`

### Установка и настройка Teamcity агентов

1. `sudo apt-get install teamcity-agent`
2. `sudo /etc/init.d/teamcity-agent install <имя_агента> <url_на_сервер>`
    - Пример: `/etc/init.d/teamcity-agent install travel-front-qyp-sas-01 http://teamcity.yandex-team.ru/`
    - Если агентов нужно несколько, запускаем команду N раз, изменяя имя агента соответствующим образом
    - Пример команды с пачкой агентов: https://paste.yandex-team.ru/5870948
3. Заводим скрипты для управления агентами:
    - В `/root/start-agents.sh` записываем содержимое из https://paste.yandex-team.ru/5871175 и проставляем права на выполнение: `chmod +x /root/start-agents.sh`
    - В `/root/stop-agents.sh` записываем содержимое из https://paste.yandex-team.ru/5871050 и проставляем права на выполнение: `chmod +x /root/stop-agents.sh`
    - В `/root/restart-agents.sh` записываем содержимое из https://paste.yandex-team.ru/5871216 и проставляем права на выполнение: `chmod +x /root/restart-agents.sh`
4. Заводим в crontab скрипты для запуска агентов после ребута и очистки docker-кэшей:
    - Редактировать конфиг: `crontab -e`
    - Записываем содержимое из https://paste.yandex-team.ru/5871250 и сохраняем
    - Посмотреть весь конфиг: `crontab -l`

### Добавление агентов в пулл Travel UI

После настройки и запуска агентов их нужно добавить в наш пулл [Travel UI](https://teamcity.yandex-team.ru/agentPool/351) в Teamcity. Это делается через чат [teamcity support](https://t.me/joinchat/AAAAAECtIetSv3Z_sqhQrQ).

Исходная [инструкция](https://ui.yandex-team.ru/ops/teamcity/new-server) от команды DataUI, которая была адаптированна под проект Travel.

## Агенты в пулле Travel UI и VM в QYP

Наши VM в QYP:

-   https://qyp.yandex-team.ru/vm/sas/travel-front-teamcity-sas
-   https://qyp.yandex-team.ru/vm/man/travel-front-teamcity-man

Наш пулл [Travel UI](https://teamcity.yandex-team.ru/agentPool/351) в Teamcity.

В пулл добавлено 12 агентов:

-   `travel-front-qyp-sas-[01-06]`
-   `travel-front-qyp-man-[01-06]`

### Возможные проблемы

1. `[Warning] IPv4 forwarding is disabled. Networking will not work` - На это сообщение обращать внимание не стоит. У нас ipv6 only.
2. `Temporary failure resolving 'mirror.yandex.ru'('dist.yandex.ru')` - Необходимо выполнить действия из [пункта 6](teamcity-agents.md/#установка-и-настройка-docker).
