# archon-devserver-command

Пакет содержит команду для [archon](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon.html),
которые запускают девсервер [kotik](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html) с необходимыми дополнениями.

## Девсервер без renderer

Подключены:

- [kotik](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/kotik) – сервер на базе express
- [tunneler](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/tunneler) – туннель до публично доступного адреса (в том числе доступен из sandbox и selenium grid)

Для подключения к проекту укажите `@yandex-int/archon-devserver-command/commands/just-kotik` в [списке команд конфига archon](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon.html#commands).

Пример конфига можно посмотреть в тесте [tutorial-project](./src/__fixtures__/tutorial-project).

Опции командной строки: `npx archon kotik --help`

```text
$ npx archon kotik --help
archon kotik

Запуск devserver на базе kotik

kotik options
  --kotik-local, -l, --local                                    Запустить без поддержки ssl и dns (только localhost)
                                                                                              [boolean] [default: false]
  --kotik-public, --public                                      Запуск с поддержкой публичной прокси
                                                                                              [boolean] [default: false]
  --kotik-cache-public-url, --cache-public-url                  Кешировать url публичной прокси[boolean] [default: true]
  --kotik-play, --play                                          Запуск в режиме проигрывания дампов данных     [boolean]
  --kotik-create, --create                                      Запуск в режиме создания дампов данных. Если дамп
                                                                существует, то он не изменится                 [boolean]
  --kotik-save, --save                                          Запуск в режиме записи дампов данных. Если дамп
                                                                существует, то он будет перезаписан            [boolean]
  --kotik-cache-file, --cache-file                              Загрузить дамп данных из файла по явно переданному пути
                                                                                                                [string]
  --kotik-required-cache-param, --required-cache-param          Если указана, дампы будут читаться/записываться только
                                                                при наличии указанного параметра в урле         [string]
  --kotik-workers, -w, --workers                                Количество воркеров Котика         [number] [default: 1]
  --kotik-port, -p, --port                                      Порт для http-сервера                           [number]
  --kotik-ssl-port, --ssl-port                                  Порт для https-сервера                          [number]
  --kotik-verbose, -v, --verbose                                Включить логирование всех событий
                                                                                              [boolean] [default: false]
  --kotik-log-time, --log-time                                  Включить логирование времени работы мидлвар и времени
                                                                обработки запроса.            [boolean] [default: false]
  --kotik-exit-threshold, --exit-threshold                      Минимально допустимое время жизни воркера после старта
                                                                                               [number] [default: 10000]
  --kotik-allowed-sequential-deaths,                            Количество последовательных падений воркера, считающееся
  --allowed-sequential-deaths                                   фатальным                          [number] [default: 1]
  --kotik-incognito, --incognito                                Не отправлять статистику использования в статфейс
                                                                                              [boolean] [default: false]
  --kotik-data-fetch-timeout, --data-fetch-timeout              Таймаут получения данных из источника в мс
                                                                                                [number] [default: 5000]
  --kotik-cache-root, --cache-root                              Директория хранения дампов данных
                                                             [string] [default: "/home/slava-b/.yandex-int/kotik/cache"]
  --kotik-template-flag, --template-flag                        Версточные флаги в формате JSON-объекта, например,
                                                                '{"f1": true, "f2": 0, "f3": "1" }'. Требует middleware
                                                                "templateFlag"                  [string] [default: "{}"]
  --kotik-check-template-flag, --check-template-flag            Проверять, что в каждом источнике есть item с типом
                                                                "flags"                        [boolean] [default: true]

tunneler options
  --tunneler-domain  Домен для генерируемых url'ов. Несколько опций будут преобразованы в список доменов.
                                                                                          [array] [default: "yandex.ru"]

dns options
  --dns-port    Порт для dns-сервера                                                            [number] [default: 3053]
  --dns-domain  Подменяемый домен. Несколько опций будут преобразованы в список доменов
  [array] [default: ["local.yandex.ru","local.yandex.by","local.yandex.ua","local.yandex.kz","local.yandex.uz","local.ya
  ndex.com","local.yandex.com.tr","local.yandex.az","local.yandex.com.am","local.yandex.com.ge","local.yandex.co.il","lo
  cal.yandex.kg","local.yandex.lv","local.yandex.lt","local.yandex.md","local.yandex.tj","local.yandex.tm","local.yandex
                        .uz","local.yandex.ee","local.yandex.fr","local.yandex.fi","local.yandex.pl","local.yandex.eu"]]
```
