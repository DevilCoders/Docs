# Локальный запуск Docker

{% note warning %}

Если возникли проблемы - [что-то пошло не так](#problems)

{% endnote %}

## Quick start

- Для начала нужно установить и настроить docker, с учётом работы IPv6
  - https://docs.docker.com/engine/install/ubuntu/
  - https://docs.docker.com/engine/install/linux-postinstall/
  - Настраиваем IPv6
    - настраиваем демон
    ```
    cat > /etc/docker/daemon.json <<-EOF
    {
    "ipv6": true,
    "fixed-cidr": "",
    "fixed-cidr-v6": "fd00::/8"
    }
    EOF
    ```
    - включаем перенаправление
    ```
    sudo sysctl net.ipv6.conf.default.forwarding=1
    sudo sysctl net.ipv6.conf.all.forwarding=1
    ```
    - Добавляем правило для ip6tables
    ```
    sudo ip6tables -t nat -A POSTROUTING \! -o docker0 -j MASQUERADE
    ```
    - Делаем правило персистентным
    ```
    sudo apt-get install -y iptables-persistent
    ```
    - Перезапускаем докер
    ```
    sudo systemctl restart docker
    ```
    - Проверяем, что IPv6 работает
    ```
    docker run ubuntu:14.04 ping6 -c5 vault-api.passport.yandex.net
    ```

- Для работы скрипта нужен клиент секретницы, устанавливаем
```
$ pip3 install --upgrade pip
$ pip3 install yandex-passport-vault-client -i https://pypi.yandex-team.ru/simple
```
Переходим в папку с таской DOCKER_HERMIONE:
```
cd arcadia/sandbox/projects/partner/tasks/docker_hermione
```
Для запуска контейнеров локально нужно выполнить команду инициализации

    arc co docker/docker-compose.yml docker/backend  docker/adfox && python3 init-local.py
Эта команда установит все секреты в докер compose, а так же в файлы настроек окружений

Так же необходимо в файл /etc/hosts прописать строку

    {IP} docker.partner.yandex.ru
    {IP} adfox-0.ci-1.docker.partner.yandex.ru

Где вместо {IP} указать IP локал хоста или qyp-машины (в зависимости того как вы настраиваете тесты)

После инициализации можно запускать контейнеры

    cd docker && docker-compose up -d --force-recreate

или
    docker compose up -d --force-recreate
в зависимости от версии Docker compose https://docs.docker.com/compose/

После поднятия контейнеров можно запускать тесты как обычно, фронтенд будет доступен по адресу
https://docker.partner.yandex.ru
Команда запуска (локально)

    E2E_BASE_URL=https://docker.partner.yandex.ru:10443/ ADFOX_HOST=https://adfox-0.ci-1.docker.partner.yandex.ru npm run test:autotests:docker:local -- --mockUrl http://docker.partner.yandex.ru:3000/api --stand https://docker.partner.yandex.ru:10443


Команда запуска (qyp)

    E2E_BASE_URL=https://docker.partner.yandex.ru:10443/ ADFOX_HOST=https://adfox-0.ci-1.docker.partner.yandex.ru npm run test:autotests:docker:local -- --mockUrl http://localhost:3000/api --stand https://docker.partner.yandex.ru:10443

***ВАЖНО**
Сейчас есть баг, что при подъеме контейнеров ADFOX стартует мок-сервис ADFOX на 3000 порту. Из-за этого нельзя полнять мок-сервис ПИ на том же порту.
Для разработки тестов ПИ, требующих мок-сервис, необходимо `docker kill` контейнеры ADFOX и запустить мок-сервис ПИ на 3000 порту.

При необходимости запускать тесты над локальным сервером - необходимо запустить его и из docker-compose.yml удалить
часть с

    frontend_node-1: ...



## Что-то пошло не так<a name="problems"></a>
- получаю ошибку `Error: image ... not found` - у вас нет прав к репозиторию. Права на чтение есть у всех в [сервисе](https://abc.yandex-team.ru/services/partnjorskijjinterfejjsjandeksa/), если вас нет в этом сервисе - добавьтесь или запросите [права отдельно](https://idm.yandex-team.ru/#rf-role=58752266#docker/distribution_prefix/partners%7C/viewer,rf-expanded=58752266,rf=1)
- запускаю на ubuntu и не запускается (например, `File already exists` или `file exists`) \
  маунтить аркадию нужно с флагом `--allow-other`\
  Чтобы он заработал, нужно разкомментировать строку в `/etc/fuse.conf`

```
# /etc/fuse.conf - Configuration file for Filesystem in Userspace (FUSE)
# Set the maximum number of FUSE mounts allowed to non-root users.
# The default is 1000.
#mount_max = 1000

# Allow non-root users to specify the allow_other or allow_root mount options.
user_allow_other                 <-- тут
```
Либо как подсказывает сам arc - выполнить команду
```
echo "user_allow_other" | sudo tee -a /etc/fuse.conf
```

Так же - arc может ругаться на отсутсвие указания стора и напишет что-то такое:
```
Store path is not specified, using last mounted: /home/omar2002/.arc/stores/_home_omar2002_arcadia_sandbox
```
Лечится добавлением параметра `-S`
```
~/arcadia$ arc mount sandbox -s /home/omar2002/.arc/stores/_home_omar2002_arcadia_sandbox --allow-other
```

Проблема заключается в том, что docker-compose запускается в рамках своей группы, а по дефолту маунт arc-а доступен
только owner-у, который маунт выполнил. В итоге папки, которые docker-compose проверяет на существование с его окружения
не существуют и он пытается их создать, но папка-то на самом деле уже есть - вот и падают ошибки про `file exist`
Флаг `--allow-other` дает возможность любому пользователю, кроме рута, читать виртуальную папку.

### No keys in the SSH Agent. Check output of 'ssh-add -l' command
```
% arc co docker/docker-compose.yml docker/backend && python3 init-local.py
Updated 0 paths from the index
/opt/homebrew/lib/python3.9/site-packages/urllib3/connectionpool.py:1043: InsecureRequestWarning: Unverified HTTPS request is being made to host 'partner.yandex-team.ru'. Adding certificate verification is strongly advised. See: https://urllib3.readthedocs.io/en/1.26.x/advanced-usage.html#ssl-warnings
  warnings.warn(
Traceback (most recent call last):
  File "/Users/daniil-belyak/arcadia/sandbox/projects/partner/tasks/docker_hermione/init-local.py", line 50, in <module>
    '{MYSQL_PASSWORD}': client.get_version('sec-01ctrfgkgnsv0bhffsq2pgm2wa')['value']['password'],
  File "/opt/homebrew/lib/python3.9/site-packages/vault_client/client.py", line 591, in get_version
    r = self._call_native_client('get', url)
  File "/opt/homebrew/lib/python3.9/site-packages/vault_client/errors.py", line 15, in wrapper
    return function_to_decorate(*args, **kwargs)
  File "/opt/homebrew/lib/python3.9/site-packages/vault_client/client.py", line 313, in _call_native_client
    for ctx in self._proceed_rsa_auth(
  File "/opt/homebrew/lib/python3.9/site-packages/vault_client/client.py", line 242, in _proceed_rsa_auth
    rsa_keys = self.rsa_auth()
  File "/opt/homebrew/lib/python3.9/site-packages/vault_client/auth.py", line 70, in __call__
    rsa_keys = self.fetch_keys()
  File "/opt/homebrew/lib/python3.9/site-packages/vault_client/auth.py", line 60, in fetch_keys
    raise ClientNoKeysInSSHAgent()
vault_client.errors.ClientNoKeysInSSHAgent: {'code': 'error', 'message': "No keys in the SSH Agent. Check output of 'ssh-add -l' command"}
```
фиксится командой `% ssh-add ~/.ssh/id_rsa` где id_rsa - ssh ключ, превязанный к стаффу
или ключ не прокинулся в qyp, нужно выйти с qyp'а через `exit` и зайти с `ssh -A <имя тачки>`

## Разработка тестов и фикстур

### Как налить конкретный тесткейс?
Нужно выполнить курл с ноутбука
```
$ curl https://docker.partner.yandex.ru:10443/testapi/wait/partner_mobile_all_blocks_inapp -s | jq
```

### Как запустить автотесты на ветке бекенда, чтобы фронт и $OTHER_BACKEND собрались с твоей ветки? 
```bash 
$ branch=`arc br | grep "*" | awk '{print $2}'`; \
    echo "{\"Front\":\"users/$USER/$branch\",\"Java\":\"users/$USER/$branch\",\"Perl\":\"users/$USER/$branch\"}" | 
    jq > `arc root`/partner/perl/partner2/test_deps/$branch.json
```
