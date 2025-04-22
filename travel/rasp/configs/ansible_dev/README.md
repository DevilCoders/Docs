# rasp-cloud-conf

Проект содержит описание конфигураций машин в разработческом облаке.
Конфигурации описаны при помощи [Ansible](http://docs.ansible.com/).
Роли находятся в **roles/**, описание хостов в **cloud-inventory**.

Условное разделение машин:

  * машины общего пользования (БД, агенты teamcity, стенды);
  * разработческие машины;

Цель:

  * быстрое воспроизведение важных машин: teamcity агенты, стенды;
  * быстрая наливка разработческих машин;

# Использование

## Подготовка к использованию (на своей локальной машине)

  * создаем и активируем virtualenv с python2.7 внутри:
    * ```virtualenv .env```
    * ```. .env/bin/activate```
  * ```svn cat svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/ya | python - clone```
  * ```cd arcadia```
  * ```./ya make -j0 --checkout travel/rasp/configs/ansible_dev```
  * ```cd travel/rasp/configs/ansible_dev```
  * ```pip install -r requirements.txt```
  * ```cp ansible.example.cfg ansible.cfg```  # ansible.cfg можно и нужно изменять под себя

**Внимание!** ansible по умолчанию будет пытаться заходить на удаленные машины используя ssh ключи для указанного в inventory `remote_user`

## Применение проектной роли к произвольной машине

Если вы не хотите разбираться в ansible и писать свои playbook'и, то эта секция для вас.
Есть возможность применить произвольную роль к произвольной машине. Для этого используется консольная утилита `iamateapot.py`.
Утилита поддерживает две комманды:

  * `list_roles` для просмотра списка всех доступных проектных ролей;
  * `apply_role {role} {host} --remote_user={remote_user} для применения выбранной роли к указанному хосту (где --remote_user - опциональный параметр, если он не указан - в качестве remote_user будет использован логин текущего пользователя);
  * все дополнительные параметры будут переданы без изменения

*Пример:*
Наливаем бэкенд морды на машину lorekhov-example.haze.yandex.net
`./iamateapot.py apply_role rasp-dev-morda-backend lorekhov-example.haze.yandex.net`

*Примеры использования дополнительных параметров.*
Наливаем тимсити-агент rasp-teamcity-myagent:
`./iamateapot.py apply_role rasp-teamcity rasp-teamcity-myagent.sas.yp-c.yandex.net --extra-vars "agent_name=rasp-teamcity-myagent"`
Наливаем тимсити-агент rasp-teamcity-myagent и устанавливаем на нем python3.7.3:
`./iamateapot.py apply_role rasp-teamcity rasp-teamcity-myagent.sas.yp-c.yandex.net --extra-vars "agent_name=rasp-teamcity-myagent" --extra-vars "python3_major_version=3.7" --extra-vars "python3_version=3.7.3"`

## Наливка разработческой машины из playbook'а

Playbook для разработческой машины по умолчанию включает окружение как для js так и для python
разработчика. Можно использовать его, а можно создать свой собственный на основе имеющихся ролей
или произвольный. Личные плэйбуки нужно хранить в playbooks/personal/<username>, они будут очень
полезны в качестве примеров.

  * Создать инвентарь (описание хостов): ```cp inventory.ex inventory```
  * Настроить инвентарь: в inventory меняем хосты на хосты своих дев машин(ы), remote_user на своего пользователя
  * Запускаем playbook ```ansible-playbook {{path_to_playbook}}``` (где path_to_playbook например playbooks/dev-node.yml)
  * ждем пока все будет сделано

## Обновление/наливка конфигураций машин общего пользования

  * Убедиться что ssh ключи есть на нужных хостах;
  * Чтобы протестировать плейбук или налить одну машину, нужно ее прописать себе в inventory, как в inventory.ex. Затем запускать нужный playbook, не забываем параметры "remote_user={{your_user}}" --extra-vars="@cloud/mysql_vars.yml"
  * Чтобы запустить на всех машинах, нужно сделать cd cloud и запустить нужный playbook указав своего пользователя: ```ansible-playbook  --extra-vars "remote_user={{your_user}}" --extra-vars="@mysql_vars.yml" {{path_to_playbook}}``` (где path_to_playbook например ../playbooks/teamcity.yml)

#### Важно!
  * Тестировать плейбуки облака через vagrant в данный момент невозможно, т.к. хаки dns64 отключают на виртуалке сеть.
  * Переменная remote_user никак не связана с опцией remote_user из конфига ansible, хотя в итоге и совпадает. Опция из конфига не прорастает в playbook и используется только в момент подключения к хостам.
  * --extra-vars="@mysql_vars.yml" нужно указывать, чтобы Rackspace ставил нужный нам mysql(на trusty по умолчанию mysql-5.5 0_0)

## Обновление рецепта для сборочного lxc контейнера

Текущая версия ресурса c ansible скриптом 1162030646, path=/tmp/ansible/
Текущая версия ресурса с собранным lxc контейнером 1162079430
Новый ресурс получаем так:

```
cd travel/rasp/configs
tar -cvz ansible_dev > ansible_dev.tar.gz
ya upload --sandbox ansible_dev.tar.gz
```

Помечаем ресурс как важный (чтобы получить ttl=infinity).
Далее используем его в задаче https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=SANDBOX_LXC_IMAGE
Можно клонировать с этой задачи https://sandbox.yandex-team.ru/task/526023024

## Наливка проекта Touch

  Перед наливкой Touch версии, убедитесь что виртуалка поднята и в нее можно ходить по SSH-ключу.
  Так же, убедитесь что вы прописали у себя в хостах дополнительные домены для Touch, вида:

  ```
  <some_ip_v6>   touch.<cloud_name>.haze.yandex.net
  <some_ip_v6>   touch.<cloud_name>.haze.yandex.ru
  <some_ip_v6>   static.touch.<cloud_name>.haze.yandex.net
  <some_ip_v6>   static.touch.<cloud_name>.haze.yandex.ru
  ```

  Зачем это нужно? Потому что базово виртуалки находятся в `.net` зоне, а Touch
  ориентируется на зоны `.ru`, `.ua`, `.com.tr`, к тому же в конфигах он явно ориентируется на
  поддомены `touch`, `static.touch`.

  Плейбук для примера запуска Touch проекта находится в `playbooks/personal/corsac/dev-touch`.
  Его можно скопировать и переделать под себя, или использовать как есть. Для установки плейбука
  нужно следовать инструкциям выше.

  *** ВАЖНО! *** - в процессе установки потребуется сходить на сервер (в отдельной вкладке терминала),
  и создать собственный ключ id_rsa. Желательно установить на ключ пароль (passphrase).

  ```
  cd ~/.ssh
  ssh-keygen -t rsa -b 4096 -C "<username>@yandex-team.ru"
  ```

  После того, как был создан ключ, нужно добавить его в ssh-agent на сервере.
  Проверяем, жив ли агент: `ps -aux | grep ssh-agent`.

  Если агентов в живых нет, запускаем агент:

  ```
  eval "$(ssh-agent -s)"
  ```

  После чего кормим ему новый ключ: `ssh-add ~/.ssh/id_rsa`.

  Отлично, ключ на сервере создан и установлен, обязательно установите ключ у себя в Github аккаунте, чтобы сервер мог клонировать проекты. Проверить все ли хорошо можно попытавшись залогиниться с сервера командой:

  ```
  ssh git@github.yandex-team.ru
  ```

  В ответ должно поприветствовать и выплюнуть обратно в консоль.

  После этого продолжаем установку рецепта. После успешной наливки машины, идем на сервер,
  в папке `touch/local_settings.py` устанавливаем доступы к базе данных и проверяем жив ли nginx.
  Если все хорошо, радуемся, запускаем Touch: `../tools/gunicorn.sh start`

# Описание ролей

## rasp-base

Базовая роль. Настраивает deb репозитории, локаль и nat64.

## rasp-dev-base

Наследует от: rasp-base.
Настраивает nginx, ставит yandex-environment, libgeobase, утилиты для сборки deb пакетов, а так же
несколько полезных утилит таких как make, tree или rsync.

## rasp-dev-js

Наследует от: rasp-dev-base.
Ставит все что нужно для разработки фронтенда.

## rasp-dev-python

Наследует от: rasp-dev-base.
Ставит все что нужно для разработки бекенда (пока без mysql!).

## rasp-mysql

Наследует от: rasp-base.
Ставит и конфигурирует mysql.

## rasp-teamcity-agent

Наследует от: rasp-dev-js, rasp-dev-python.

# Vagrant**

*Пока не работает из коробки, т.к. dns64*

Тестировать конфигурации удобно на виртуалке на локальной машине. Для этого можно использовать Vagrant:
  * ставим Vagrant
  * в inventory в [dev-node] ставим хост вида "192.168.33.11 remote_user=vagrant". Этот IP прописан в файле Vagrantfile.
  * vagrant up  # вся магия находится в файле Vagrantfile. Будет скачан нужный образ виртуалки (при первом запуске),
поднята машина, и применен плейбук playbooks/dev-node.yml
  * vagrant ssh # заходим по ssh на виртуалку и проверяем всё
  * vagrant provision  # заново применяем плейбук на машине
  * vagrant destroy # убиваем виртуалку. Следующий vagrant up создаст чистую машину

# Прочее

  * Документация по ansible: http://docs.ansible.com/
  * Роли https://galaxy.ansible.com
