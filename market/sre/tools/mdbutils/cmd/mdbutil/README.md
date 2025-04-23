1. Добавление хоста в локацию.
```
./mdbutil add-hosts --clusters-ids mdb8q613r16s0484kgsi@mongo --locations vla --doit
2022-04-15T12:57:18.759+0300	INFO	mdbutil/mdbutil.go:89	[init] enable info mode
2022-04-15T12:57:19.270+0300	INFO	mdbutil/mdbutil.go:322	[mongoAddHost] в кластере mdb8q613r16s0484kgsi заведены хосты: host: sas-c57i723rpa40z3it.db.yandex.net, health: ALIVE, location: sas
2022-04-15T12:57:19.270+0300	INFO	mdbutil/mdbutil.go:323	[mongoAddHost] в кластер mdb8q613r16s0484kgsi будут добавлены хосты для локаций: vla
2022-04-15T12:57:50.124+0300	INFO	mdbutil/mdbutil.go:222	operation waiting, done: false, error: %!s(<nil>)
...
2022-04-15T13:06:20.124+0300	INFO	mdbutil/mdbutil.go:215	operation success, done: true
```

2. Удаление хоста из локации.
```
./mdbutil delete-hosts --clusters-ids mdb8q613r16s0484kgsi@mongo --locations sas --doit
2022-04-15T13:38:49.438+0300	INFO	mdbutil/mdbutil.go:89	[init] enable info mode
2022-04-15T13:38:49.903+0300	INFO	mdbutil/mdbutil.go:358	[mongoDeleteHost] в кластере mdb8q613r16s0484kgsi будут удалены slave хосты: [sas-c57i723rpa40z3it.db.yandex.net]
2022-04-15T13:39:20.600+0300	INFO	mdbutil/mdbutil.go:222	operation waiting, done: false, error: %!s(<nil>)
2022-04-15T13:39:50.601+0300	INFO	mdbutil/mdbutil.go:215	operation success, done: true
```

3. Удаление хоста из локации, если он мастер.
```
./mdbutil delete-hosts --clusters-ids mdb8q613r16s0484kgsi@mongo --locations vla --doit
2022-04-15T13:49:01.877+0300	INFO	mdbutil/mdbutil.go:89	[init] enable info mode
2022-04-15T13:49:02.338+0300	INFO	mdbutil/mdbutil.go:358	[mongoDeleteHost] в кластере mdb8q613r16s0484kgsi будут удалены slave хосты: [vla-sr44sj1zo6sast74.db.yandex.net]
2022-04-15T13:49:33.260+0300	INFO	mdbutil/mdbutil.go:222	operation waiting, done: false, error: %!s(<nil>)
2022-04-15T13:50:03.260+0300	INFO	mdbutil/mdbutil.go:215	operation success, done: true
2022-04-15T13:50:03.260+0300	INFO	mdbutil/mdbutil.go:376	[mongoDeleteHost] текущий мастер [vla-0brzt9mn1iq8uroc.db.yandex.net] находится в удаляемых локациях vla
2022-04-15T13:50:03.260+0300	INFO	mdbutil/mdbutil.go:378	[mongoDeleteHost] в кластере mdb8q613r16s0484kgsi будут переключены и удалены хосты: [vla-0brzt9mn1iq8uroc.db.yandex.net]
2022-04-15T13:50:03.260+0300	INFO	mdbutil/mdbutil.go:381	[mongoDeleteHost] пытаемся сменить мастера
2022-04-15T13:50:23.585+0300	INFO	mdbutil/mdbutil.go:387	[mongoDeleteHost] удачная смена мастера
2022-04-15T13:50:54.080+0300	INFO	mdbutil/mdbutil.go:222	operation waiting, done: false, error: %!s(<nil>)
2022-04-15T13:51:24.080+0300	INFO	mdbutil/mdbutil.go:215	operation success, done: true

```
