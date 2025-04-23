# surfwax-agent

Агент для отправки статуса selenoid в surfwax-coordinator.

## Использование

Запуск:

```
$ npx @yandex-int/surfwax-agent [options]
```

Принудительная остановка по `Ctrl + C` (или сигналами `SIGINT`, `SIGTERM`).

Полный список опций:

```
Options:
  --help                             Show help                         [boolean]
  --version                          Show version number               [boolean]
  --quota                            Quota identifier        [string] [required]
  --browser-group                    Browser group        [string] [default: ""]
  --secret                           Quota secret            [string] [required]
  --listen-port                      Agent port to listen    [number] [required]
  --listen-host                      Agent host to listen    [string] [required]
  --lifetime                         Agent lifetime, seconds [number] [required]
  --coordinator-endpoint             Coordinator host and port          [string]
  --coordinator-deploy-stage         Coordinator stage in Deploy        [string]
  --coordinator-deploy-unit          Coordinator deploy unit in Deploy  [string]
  --coordinator-deploy-dc            Coordinator DC in Deploy            [array]
  --coordinator-update-interval      Coordinator update interval, seconds
                                                           [number] [default: 3]
  --selenoid-endpoint                Selenoid host and port  [string] [required]
  --selenoid-poll-interval           Selenoid polling interval, seconds
                                                           [number] [default: 3]
  --selenoid-start-timeout           Selenoid start timeout, seconds
                                                         [number] [default: 180]
  --selenoid-status-timeout          Selenoid status timeout, seconds
                                                          [number] [default: 30]
  --selenoid-create-session-timeout  Selenoid create session timeout, seconds
                                                          [number] [default: 60]
  --session-shutdown-timeout         Timeout to wait for session on shutdown,
                                     seconds
                                                          [number] [default: 60]
  --selenoid-proxy-timeout           Selenoid request proxying timeout
                                                          [number] [default: 120]
```

При запуске агент регистрируется в координаторе и начинает поллинг статуса selenoid по указанному адресу. Полученный статус отправляется в координатор вместе с адресом selenoid и адресом агента, на котором слушает специальный прокси сервер, проксирующий запросы создания сессий. При остановке (или после `lifetime` секунд с момента запуска) агент "разрегистрируется" на координаторе и завершает работу.

По умолчанию, агент не имеет никакого вывода. Отладочный вывод можно включить с помощью переменной `DEBUG`:

```
DEBUG=surfwax-agent,surfwax-agent:*,si.ci.requests ...
```

## Публикация новой версии

### Пререквизиты

- запросить роль [разработчика](https://abc.yandex-team.ru/services/surfwax/?scope=development) SurfWax с помощью [IDM](https://idm.yandex-team.ru)
- [установить](https://docs.docker.com/engine/install/ubuntu/) docker
- [установить](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#ya-setup) ya

### Сборка кода

В корне `surfwax-agent`:
- `arc checkout trunk && arc pull trunk`
- `npm run build`

#### Сборка образа

- удалить tar-файл, созданный при выкатке предыдущей версии:
    ```bash
    $ rm -f *.tgz
    ```
- опубликовать новые образы:
    ```bash
    $ make docker-publish
    ```

#### Сборка кэша слоёв для podman

- Создать задачу `SURFWAX_BUILD_LAYERS_CACHE`, [пример](https://sandbox.yandex-team.ru/task/1007279350/view)
- Выбрать в `Layers cache type` значение `Surfwax agent`, в `SurfWax agent version` указать свежезапушеный тэг
- Запустить, дождаться ресурса `SURFWAX_LAYERS_CACHE`
