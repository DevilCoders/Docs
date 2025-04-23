## rttctl spawn

Spawn new RT and some other project test env

```
rttctl spawn [flags]
```

### Examples

```

Simple create from RT branch:
	rttctl spawn --rt.branch=mybranch
Create from RTAPI repo
	rttctl spawn --rtapi.branch=mybranch
Create on node n7:
	rttctl spawn --node="name=n7.*"
Create from Rtapi MR:
	rttctl spawn --mr 7 --mr-project nocdev/rtapi2rr
Alpha version of multienv:
	rttctl spawn --slaves 1

```

### Options

```
      --branch string           Ветка RT
      --commit string           Коммит RT
      --cvs-snap string         Создать окружение на указанном снимке CVS
      --envid string            id существующего окружения
  -h, --help                    help for spawn
      --invapi.branch string    Ветка invapi
      --invapi.commit string    Хеш конкретного комита invapi
      --invapi.project string   ID или имя проекта invapi
      --labels stringToString   Метки окружения, --labels="l1=2,l4=g" (default [])
      --master string           Создать дополнительное окружени к мультиокружению
      --mr string               Номер MR
      --mr-project string       ID или имя проекта, для которого нужен MR (default "nocdev/racktables")
      --multi                   Искать по мультиокружениям в том числе
      --mysql-snap string       Создать окружение на указанном снимке MySQL
      --nortapi                 Не запускать RTAPI
      --notest                  Не будет тестов
      --noweb                   Не запускать веб-морду
      --prj string              Основной проект, rt или rtapi (default "rt")
      --project string          Проект RT
      --rt.branch string        Ветка rt
      --rt.commit string        Хеш конкретного комита rt
      --rt.project string       ID или имя проекта rt
      --rtapi.branch string     Ветка rtapi
      --rtapi.commit string     Хеш конкретного комита rtapi
      --rtapi.project string    ID или имя проекта rtapi
      --rw                      перевести в RW
      --slaves int              Запустить окружение со несколькими slave
      --sync                    Дождаться запуска
      --ttl duration            Время жизни окружения. (default 168h0m0s)
      --update                  Если есть - обновить
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

