## Экстренная выкладка ya-salt стейта при недоступости VCS

### Подготавливаем данные и поднимаем hm-server'ы

* Находим список мастеров для машин требующих выкладки

```
ssh {target_host} cat /etc/salt/minion.d/runtime.conf
```

* Копируем директорию с мастера на локальный хост и вносим изменения

```
rsync -LaH --rsh=ssh {hm_server_host}:/var/lib/repo/current/ salt
vim salt/some/state.sls
```

* Чтобы контроллировать изменения можно (опционально) инициализировать
  репозиторий, в дальнейшем это так же позволит сформировать патчи для VCS

```
cd salt && git init && git add * && git ci -a -m 'original version'
```

* Очень желательно прогнать тесты

```
См README.md#Testing в скачанной директории
rm -rf venv  # until HOSTMAN-231 is not fixed
```

Далее все действия выполняем c группой мастеров которые должны отдавать новые
данные

* Раскладываем подготовленную директорию

```
rsync -aH --rsh=ssh salt/ root@{hm_server_host}:/opt/yandex-hm-server/emergency.d
```

* Выключаем ya-salt на хостах hm-server'ов

```
# FIXME: сделать опцию на сколько отключать - 2 часa тут может не хватить.
# * за состоянием хостов hm-server'а и статусом демона тоже следит салт.
sudo ya-salt disable
```

* Запускаем замещающий сервер, который будет раздавать файлы из созданной
  директории

```
sudo systemctl start yandex-hm-server-emergency.service
sudo systemctl enable yandex-hm-server-emergency.service
```

  * `enable` нужен только для того чтобы пережить ребуты.
  * При активации `yandex-hm-server-emergency.service` продакшен инстансы
    `hm-server`'а будут остановлены и деактивированы.

### Возвращаемся к штатному режиму

* Переносим изменения в репозиторий, создаем PR и мержим в нужные ветки

Детали веток, коммитов, тестов и мержа описаны в
[README.md](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/browse/README.md)
salt репозитория.

* Возвращаем hm-server'ы к исходному (продакшен) состоянию

```
sudo systemctl stop yandex-hm-server-emergency.service
sudo systemctl disable yandex-hm-server-emergency.service
sudo ya-salt enable
sudo ya-salt run --no-orly  # поднимет продакшеновый инстанс hm-server'а
sudo rm -rf /opt/yandex-hm-server/emergency.d/
```
