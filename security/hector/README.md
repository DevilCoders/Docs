Hector
=====

Небольшой утиль для запуска разных задач над Github/Bitbucket репами и paste.y-t.ru.
Как работает, на примере GH:
  - идет в GH с переданным токеном;
  - выгребает все репы;
  - если не передан ключ `--use-ssh`, исключает приватные, т.к. для их чекаута нужен ключик;
  - отсекает те что не подходят по фильтру языков или слишком здоровенные;
  - делает shallow чекают;
  - запускает указанный бинарь с аргументами и путем к папке с репо;
  - результат пишет в файл `{{work}}/{{org}}:{{repoName}}.json`.


### Usage
Удобнее всего, базовые вещи определить в конфиге `~/.hector.{toml|yaml|json}`, например:
```toml
# Токен для GH, получать тут: https://github.yandex-team.ru/settings/developers
GhToken = "my-gh-token"

# Куда чекаутить репы 
Work = "/mnt/tmpfs"

# Куда складывать результаты
Result = "/srv/results"

# Фильтруем по языкам, т.е. берем репы у которых не менее 70% процентов кода написано на JS или 50% на питонячке
Languages = ["javascript:70", "python:50"]

# Бинарь для запуска
CheckCommand = ["yadi", "test", "--format", "json", "--recursive", "--remote"]
```

А уже потом по желанию переопределять нужные параметры, например, запустим с другим бинарем:
```
$ hector gh -- ant-secret -format=json
Using config file: /home/buglloc/.hector.toml
2017/07/28 13:45:38 Removed repo directory '/mnt/tmpfs/slovari/www'
2017/07/28 13:45:38 Skip by language filter 'qatools/junitextensions'
2017/07/28 13:45:38 Removed repo directory '/mnt/tmpfs/snews/www'
2017/07/28 13:45:38 Complete repo: usertime/ffsocat
2017/07/28 13:45:38 Complete repo: slovari/configs
2017/07/28 13:45:38 Complete repo: usertime/server
2017/07/28 13:45:38 Complete repo: tools/cbb
2017/07/28 13:45:38 Complete repo: Wordstat/pokazometer
...
```

### Результат работы
Для каждой репы Hector создаст файлик `{{work}}/{{org}}:{{repoName}}.json`, следующего содержания:
```json
{
  "repo": {
    "name": "dafgar/MPFS",
    "parent": "MPFS/MPFS",
    "url": "https://github.yandex-team.ru/dafgar/MPFS",
    "clone_url": "https://github.yandex-team.ru/dafgar/MPFS.git",
    "private": false,
    "owners": [
      "dafgar"
    ]
  },
  "work_dir": "/mnt/tmpfs/dafgar/MPFS",
  "ref": "master",
  "result": {
    "stdout": "",
    "stderr": "...",
    "exit_code": 0
  }
}
```

По умолчанию Hector не парсит stdout дочернего приложения.

Если это необходимо, например, для того что бы Hector смог определить авторов строк, сделать красивые линки на файлики и т.д. - можно передать параметр `--parse-stdout`, но тогда дочерняя программа должна делать вывод в формате подходящем для Гектора:
```json
[{
  "path": "/some",
  "line_no": 0,
  "problem": {}
}]
```

Например, в случае AntSecret'а:
```json
[
  {
    "path": "/home/buglloc/work/projects/ant-secret-test/ignore/settings.py",
    "line_no": 243,
    "problem": {
      "plugin": "Tokens",
      "message": "YT_TOKEN = eda335bdb8a221dd976a67714a58bb05a",
      "additional": {
        "extracted": "eda335bdb8a221dd976a67714a58bb05a",
        "sha1": "196d82bc1827050e2a224ad9868b912b26183c00"
      }
    }
  },
  {
    "path": "/home/buglloc/work/projects/ant-secret-test/ssh/id_rsa",
    "line_no": 0,
    "problem": {
      "plugin": "Keys",
      "message": "TLS/SSH Private Key",
      "additional": {
        "fingerprint": "cb:54:82:99:8d:c2:0e:b0:39:1e:1f:b3:ea:2a:14:37",
        "fingerprint_sha256": "SHA256:UZUPIl6ZFvwSpuPVOxnfx9WpV/78wxh1x2u40p8gnOU",
        "sha1": "4c8bacda6d091ad9377b611ee0deb561d343496b"
      }
    }
  }
]
```

### Где взять?

  1. Установить из pypi: `pip install hector-bin -i https://pypi.yandex-team.ru/simple/`
  2. Скачать с [https://tools.sec.yandex-team.ru/hector](https://tools.sec.yandex-team.ru/hector)
  
### Текущий статус

Причесывается