Программа для получения списка сервисов из market-map,
связи компонент с родительскими сервисами и проставления руководителей.
При желании полученный результат можно сохранить в CVS файл.

Пример:
1. CSV:
``
./abctool generate --csv /tmp/abc.cvs
2022-04-07T16:51:31.578+0300	INFO	cmd/main.go:95	start getting person_head for componets
2022-04-07T16:51:31.848+0300	INFO	cmd/main.go:157	name: contentapiadmin, component: contentapiadmin(dimkarp93), service: marketapi(dimkarp93)
2022-04-07T16:51:31.848+0300	INFO	cmd/main.go:199	finish getting person_head for componets
2022-04-07T16:51:31.848+0300	INFO	cmd/main.go:91	safe csv file /tmp/abc.cvs success
``

2. EXEL:
``
./abctool generate --exel /tmp/abc.xlxs
2022-04-07T16:45:10.791+0300	INFO	cmd/main.go:92	start getting person_head for componets
2022-04-07T16:45:11.124+0300	INFO	cmd/main.go:153	name: contentapiadmin, component: contentapiadmin(dimkarp93), service: marketapi(dimkarp93)
2022-04-07T16:45:11.129+0300	INFO	cmd/main.go:194	safe exel file /tmp/exel1.xlxs success
2022-04-07T16:45:11.130+0300	INFO	cmd/main.go:197	finish getting person_head for componets
``
