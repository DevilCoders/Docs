## rttctl ps

list RT test env

```
rttctl ps [flags]
```

### Examples

```

List env for MR 100500:
	rttctl ps --mr 100500

```

### Options

```
      --branch string           Ветка RT
      --commit string           Коммит RT
      --envid string            id существующего окружения
  -h, --help                    help for ps
      --invapi.branch string    Ветка invapi
      --invapi.commit string    Хеш конкретного комита invapi
      --invapi.project string   ID или имя проекта invapi
      --labels stringToString   Метки окружения, --labels="l1=2,l4=g" (default [])
      --mr string               Искать по номеру MR
      --mr-project string       Искать по ID или имени проекта MR
      --multi                   Искать по мультиокружениям в том числе
      --nortapi                 Искать окружения созданные без RTAPI
      --notest                  Искать окружения созданные без тестов
      --noweb                   Искать окружения созданные без веб-морды
      --prj string              Основной проект, rt или rtapi (default "rt")
      --project string          Проект RT
      --rt.branch string        Ветка rt
      --rt.commit string        Хеш конкретного комита rt
      --rt.project string       ID или имя проекта rt
      --rtapi.branch string     Ветка rtapi
      --rtapi.commit string     Хеш конкретного комита rtapi
      --rtapi.project string    ID или имя проекта rtapi
```

### Options inherited from parent commands

```
      --dc string             DC filter, dc1,dc2,!dc3
  -d, --debug                 debug mode
      --dev                   connect to dev instance.
      --env string            Main staging instance or dev. (default "stage")
      --gitlab_token string   gitlab token
  -j, --json                  JSON output
  -n, --node stringToString   Node filter, --node="name=n1.*" (default [])
      --rttctl_host string    host (default "test.racktables.yandex-team.ru")
      --rttctl_token string   token for RT staging API
  -t, --timeout duration      Query timeout (default 1m0s)
```

### SEE ALSO

* [rttctl](rttctl.md)	 - Manage RT test env

