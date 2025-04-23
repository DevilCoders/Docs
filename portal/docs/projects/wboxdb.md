## Что это такое

**widb** - хранилище виджетов
**wboxdb** - хранилище пользовательских настроек

## Как выглядит

Виджеты
![виджет](https://jing.yandex-team.ru/files/cheetah/Снимок%20экрана%202021-07-09%20в%2013.37.14.png)
Дополнительно в хранилище пользовательских настроек находится:
 - настройка города погоды
 - настройка котировок
 - настройка любимой рубрики новостей

## Исходный код

[github](https://github.yandex-team.ru/morda/portal-morda-wboxdb)
[добавить mysql ноду](https://github.yandex-team.ru/morda/portal-morda-wboxdb/blob/master/cloud/tmpls/variables.tmpl)

## Алерты

#### Проверки со стороны бекендов
https://juggler.yandex-team.ru/aggregate_checks/?project=portal&query=host%3Dportal.wb*_cloud

 - mysql_role проверяет доступность каждой нод MySQL, алертит при потере связи
 - mysql_response прогоняет простой тестовый запрос через весь контур: бек - haproxy - mysql; проверяется наличие критерия хорошего ответа
 - wboxdb_error_log парсит лог бекенда, новые ошибки приходят в виде агрегированных по бекам сообщений в чат

#### Проверки со стороны awacs балансеров
https://juggler.yandex-team.ru/aggregate_checks/?project=&query=host%3Dawacs.stable-wb*

#### Исходники
[github](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/wboxdb.py)



## Инфраструктура

### Продакшн

#### Схема

![Итоговая схема](https://jing.yandex-team.ru/files/cheetah/Снимок%20экрана%202021-07-09%20в%2013.48.49.png)
[схема в drawio](https://drawio.yandex-team.ru?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1#R7V1fd5u4Ev80Oefeh%2FiABAI%2FOnGS7jbttjfd9nZferBNbG4xZDFu7P30VwIJ0B8bTACT2Ok5rhgJ2Wh%2BmhmNRsMFvF5u7iLnafEhnLn%2BBdBmmws4vgBAtwyE%2FyOUbUoZDq2UMI%2B8GW2UEx68f1xK1Ch17c3cFdcwDkM%2F9p544jQMAncaczQnisJnvtlj6PPf%2BuTMXYnwMHV8mfrNm8WLlGoDK6e%2Fc735gn2zjoZpzdJhjemTrBbOLHwukODNBbyOwjBOS8vNteuTwWPj8u237Tf%2F%2Fie6%2B%2F3z6m%2Fnz6v3Xz5%2BvUw7uz3kluwRIjeIa3f9%2Bc%2F379eevR5%2Bvfo6W%2Bgzf%2Fb5r0tAH%2FaX46%2FpgH10gmBLnzjesmGMwnUwc0lX%2BgW8el54sfvw5ExJ7TMGDqYt4qVPqx%2FDIKZI0PEwXc19Z0XYqOHyKo7CnxkrSOtsXEm143vzAJd99zEmPXm%2Bfx36YZT8Cvhokn9ZL4UalPzR7y7Q0z9MrziGdKx%2FuVHsbgoIomN654ZLN47w%2BGi01qbooNPDYNfPOdgsRGmLAtCAQYkOBfg86zpnIi5QPh7AU1OXeHoBkB%2FTweH4iv5eh6zicpWwbIQb2E%2BbvA6X5vR%2FZ0k4HUxWT8k17siZ%2BO6P50m4mU1%2BLJ1V7EY%2F1vOIfd8kOvRmNw4PutnLblXe5qf%2F36YPzsi9xPbMdO2ZocK2DSYwwfYK%2FyovmNPu2kK0DgRID2VIQ1MFaa0BSMM765fzbnO3%2Fet%2B%2BMddHMT%2F0f64hApEN8VEdBgTRa45rv04VUqkqe1OHgtsn2I%2BYZhmbLxPYDA2WmQlACbHStOSWZkJoiIr9SZYqZROFlJJJ35644Ee3pLPq5vkE1P0C%2Fs6KVsFOkg%2BtaQ2LZusPf60ezrR%2B6%2FE9Io6rEWUKHUYh5KznfIiFptH5zEE5ZKAqKJS0j2sZDJUJV2V9zb6Nrp%2BOGOvJvag0SX2lI%2BgMCiI0tELSmTElIiWFK6Z3sG6JqUYSfl45qTI98dHMFVaIjM0QSZqkb9wKAgXxSIosyqLDG5iDaR%2BhEqy5cO4r4uB%2Fk%2FibMIeT4Fo5asCPORPpLhe%2BqNpTMbqijyxN3X8e2fi%2Bp%2FClRd7IWHEJIzjcIkb%2BKTiypn%2BnCdY4KcY%2Fiv0MaJMjEMBGOE69r0A8405tdpcsBmifFWs1xSMQa0Zb%2BV8cYPZiDj38NWUzBlvyo8fHqFo%2B18ybgOTXX6nw5hcjDfc1ZZdbby4cBu%2B%2Bs56xOX8JnKxrcWWVbiOpm65aomdaO7Ge0bJoB26M86BKXO5wEbVqpvRItd3Yu8X7%2FZU8ZZ%2Bw6fQS5xBmQznl4oSPNIHp3cV%2FYxCR4YhdKQLHaUjI3WUQC177ProU4v%2Bg9xfurbD%2F5X0gpfvAaO9%2B%2FLlk8JcTBequfupeAtbs%2BLP24I1kVoWOrMpUuKYNqaXFn9vYp7kd11X9XdhsRLz043XMkEYuIJKoiTJlSEKwqU3m5GvUSrOXLW2KQ0hBAMBgQpzROX0AG0JRKDyeYgSEYuBB3oZRvEinIeB49%2FkVGH48jb3IdE%2BCR%2F%2F58bxlhokzjoOeS4fNuKlAgzAigLshZLJ1Hj1ZosCZYdkakygmBL3PmwfPt%2FL837lO%2Fgpz%2BsBQ7MHBm8tKnzIutXSikDNxSaskhrWRV1Lpr5Vonx8tqtZOquh0SuzxNAEWW7VNEuAYN9kOxhdmSX2TrMktQ7qmiV1TJBGvriuIYPpluSyHzNzJqHs%2BtknZcggndd7xzdjZK%2FZWRHuZ6GwlXp8NQgaVIOs%2FJ1TiWVqkFOCuU5sRA2Wajdmy%2FVEu0HEK6Wqpq3ckeACsu1utRuzGhpfdKfRIZfreXSJf%2Fpg62AJshkEbiwLHdrUjcPyph5uqG7Ul2CR%2BnEG1KPcXZQBgjz4oGJvUVd5IEWQNiblmG%2BtLTimEUeHoJLeURmctP0bx%2BgijLx%2F8Pc7mf3WXWiMVQG0TDx3A1o5FvNw1fxiv7nVheN876QtKnFlNBgLWu2LEjd5JW6woKuDPeeCo8vs2HNuqDznnQMQvAIAol4B0NAFHwms6yOxLMF1boqbty1D0FRFenYRu1wvaLlGtPIJhCm3pbLFfe5uA5PVIkO17jkhnc3WfaUi0%2BjXwhuZApTqikxL2O3uWmdDlVv5hHR2dQCCXgHQFJ27dQGIjgxAU5aAO5zC7JhOPxarR%2FQK68JW1PG9wqZq6Xmgv8RQ2V1jN3anMeYuOU9J2D%2FAJT%2BcOv4iXOEGIwi1YesG0MuO%2BFRAyjGP%2BEBh%2FivABFSxt61tEzEJ%2Bfbj%2F%2FadVSvdimCCsycKCQgx3FbdrQgwNAda4Q9w3aJht%2BqpCZ%2Fay6I%2BQEdhH2pPBaiKxn751IAlSDUxWqO6S2PI469j8wipdiK6BaB1VADarxOAki%2B2LgChEMCU2etdARCctjZuPJq1KweF1Yw6RohXxzrXrS1agW2jUX3wbqQXgsmuC6e6by9oxJheOPCdRowhVTOt0OCWOwueH%2BnTJPy%2F7TgySxBlluJ8kK53uUJACq8pOX55UwgLzFidUEAxtjC7LCJFZ%2FdmKMiOTdzycYkZKEyGGlioui18r10ITUwzDgwPAxppiQr07DSpEA%2BpRHf2w24qf2lyy2mhW1q3KNDdbZgkks8LJOjWOC7l8q6Y3WJMw2ZzrO2CeQZSrTSad5pylXhpovnE%2BVcCO4AfTlOW%2Fk2KybZV4uJ5dJaev01vX4ZBuEq4zDXJvUBJ0AytSjBxmTZPKoMwQYZic84UE5CZeLwJNcmulV2x8TcTDmDKmJTJDzfJiJuYbWVt9awtw2KtbkDeTcrmrAZ%2FjElPI52VyDSnpWueRpoQ3WWC%2FDK%2FLeuKCCpaQuUdaIrbbrPSVVays9KI65Q%2BVgqj7LESIYKvUjFCyHpyWRQlhJpIDlKRixOOnIoUQqJChRB5sUIqqWAhlQXRQmpSCJm5eCFELaEUeJKKjypcz6oyhucyxiRSJmuZ6FHWzTanI6tAT6VO3rteqKPSJwdRoQ5LoYw%2BL%2FwAEY%2FJZQbKIpGfKrSdNKfOgfUkrKt3BpF8QDA91nFSfIFCtipDEZLXrSaXg%2BVPkC3I6htbFE7d8Tl7S13%2BmgJ%2FO83eok4gIfus3o0%2BReFGzvf1tqeeKBFV%2Bfs6nXpWhXink8i5YopnHhShaArGtJdzRbHoPE3G9C0ZTj%2By4ZjFw3r6gPiB924f4YtPbuThMSCysY3ILZYItOiZ35dQpyeOeShoy8u6jnlDkO2XIgRbdsVbvYgcRNZQAKbVR2DutUN7gkxjaA0g2rXTowN9YA8Lf3ZN2AqLZ73jgA4m3oU1mZyN821bhqZwsjwz0DuwDJUbraqgryYiCGkwqfYxnLl6zyMFe54MXIgURArIqBI4NrHMU0KmgslaXQFx6qc0rUCdFAb11cy%2BCVMauK7367CZmCfQqhu4DoUI%2BBYjA%2FeOa6sSC5wl1kvcH3rPJJYyiVjTmIFnzLwoF3XfMNPoOuvVqTldsZraO7f6oueEuE1LPENaWc%2BBko5a1nMMbgX8PbkRuW3iTH82J1Re7f5HhhjmZFe8nsBUJAJpbSkF5BiuDrLD1gnWFZVKw7KDQbc8IQOoKDsqC4WXMVA2LYO5F2zOk02ebNqxJ9vJ5IXdC9XmplhHB4RsKVVJ3YT1UDzq0fFCFMgG4llBcya9eBjs6ApaDkA5y%2FcdvDq2fGfuqRM9%2F8SgWi7f7V7Jd0ODAzHuTFyiV96y0sU3QrSYJGPvKbTzC0wPFCemJb5JwERDxsxOXmKq5qe8pm48X0aSQ%2FucLqPx8CAJULYSUG2lzFDjqcILjt9ymoLKmRfZxOuJlkJAQpORoengk7oQCJ0hTeqsbUXVRD67V5yugOXze21AtEzYIBBNEdXIMLoGohwccJoh4KiiBdRpsA%2FsYu%2F8HO3TrKGDdBVuOt0LhY0GQ3N64jXshcKqzlbYr8W4ZUjvcwP1tQsSVRWyOzdzdr%2BM6xz70w%2F5hVAf5VdbeTLP8T%2BNZbuRZFUPcGM06oR%2BfXpPkQRu7%2Fzqid5TLISG9fWeZMgrOmtZ7ynei3TeauS0jiato6FKenS6haV4L8t5u3EXv4zh8fl1fG%2FuUX1ooKK0Z9KoL9Le0AZ8sljTfIEPTRIkna9yFC8nOUt7zlaU3fc9kPay5%2FMs7Xfxqw%2FSXuULrW3bv7oAEwbXcmnfr3z3lmkNhONFBqwt7i1kirqjwb27C5rdrdA8z%2BsGb%2F4P)

#### Таблица
{% note alert %}

Переименование сервисов в nanny без правки конфигов запрещено!

{% endnote %}
| Awacs балансер                | Nanny сервисы | L3 | Доступы |
|  ---------------------------- | ------------------------------------------------------------ | ----------|-------|
| [stable-wboxdb-ugr](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/stable-wboxdb-ugr/show/)  | [stable_wboxdb_ugr](https://nanny.yandex-team.ru/ui/#/services/catalog/stable_wboxdb_ugr/) | wboxdb-ugr-int.yandex.net | [puncher](https://puncher.yandex-team.ru/?id=603d5229c11b93bd179f6891) |
| [stable-wboxdb-master-ugr](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/stable-wboxdb-master-ugr/show/) | [stable_wboxdb_master_ugr](https://nanny.yandex-team.ru/ui/#/services/catalog/stable_wboxdb_master_ugr/) | wboxdb-master-ugr-int.yandex.net | [puncher](https://puncher.yandex-team.ru/tasks?id=606466e87aec9cd3531432f5) |
| [stable-wboxdb-eto](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/stable-wboxdb-eto/show/) | [stable_wboxdb_eto](https://nanny.yandex-team.ru/ui/#/services/catalog/stable_wboxdb_eto/) | wboxdb-eto-int.yandex.net | [puncher](https://puncher.yandex-team.ru/?id=6051db084c3d2ab4c6b234ef) |
| [stable-wboxdb-master-eto](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/stable-wboxdb-master-eto/show/) | [stable_wboxdb_master_eto](https://nanny.yandex-team.ru/ui/#/services/catalog/stable_wboxdb_master_eto/) | wboxdb-master-eto-int.yandex.net | [puncher](https://puncher.yandex-team.ru/tasks?id=606467187aec9cd3531432f6) |
| [stable-widb](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/stable-widb/show/) | [stable_widb](https://nanny.yandex-team.ru/ui/#/services/catalog/stable_widb/) | widb-int.yandex.net | [puncher](https://puncher.yandex-team.ru/?id=6051db32601b4f84ea48f128) |
| [stable-widb-master](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/stable-widb-master/show/) |  [stable_widb_master](https://nanny.yandex-team.ru/ui/#/services/catalog/stable_widb_master/) | widb-master-int.yandex.net | [puncher](https://puncher.yandex-team.ru/tasks?id=606467ca7aec9cd3531432f7) |

#### Дашборд выкладки

[nanny dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/morda_wboxdb/)

#### Yasm панели

[widb](https://yasm.yandex-team.ru/template/panel/WIDB_MIGRATION/)
[wboxdb eto](https://yasm.yandex-team.ru/template/panel/WBOXDB_ETO_MIGRATION/)
[wboxdb ugr](https://yasm.yandex-team.ru/panel/cheetah._xGvUkQ/)
[мониторинг баз со стороны морды](https://yasm.yandex-team.ru/template/panel/morda_subreqname/alias=wboxdb/)

#### Sandbox ресурсы

[PORTAL_MORDA_WBOXDB_TARBALL](https://sandbox.yandex-team.ru/resources/?type=PORTAL_MORDA_WBOXDB_TARBALL)

#### MySQL базы

[stable-wboxdb-eto](https://cloud.yandex-team.ru/folders/foocqso83qg8i157m8tr/managed-mysql/cluster/mdbckvng7v5d9n0f60i8)
[stable-wboxdb-ugr](https://cloud.yandex-team.ru/folders/foocqso83qg8i157m8tr/managed-mysql/cluster/mdbs65f7ak95mpc3k9tg)
[stable-widb](https://cloud.yandex-team.ru/folders/foocqso83qg8i157m8tr/managed-mysql/cluster/mdbf43e06tusrpong9so)

#### Пароли от баз

[yav](https://yav.yandex-team.ru/secret/sec-01ez01bwvn1v230fga0ndry7jz)


## Как чинить

#### Пользователь для диагностики

[yav](https://yav.yandex-team.ru/secret/sec-01fb1wjdn2etqd8zqm6x9jjy9r)

#### Как добавить хост в MySQL кластер

1. [Выбираем кластер из списка](https://docs.yandex-team.ru/portal/projects/wboxdb#mysql-bazy)
2. Заходим на главную страницу для управления MySQL кластером
![главная](https://jing.yandex-team.ru/files/cheetah/Screenshot%202021-07-20%20at%2015.31.42.c13ec3a.png)
3. Выбираем пункт для добавление хоста
![хосты](https://jing.yandex-team.ru/files/cheetah/Screenshot%202021-07-20%20at%2015.34.45.a263204.png)
4. Выбираем датацентр и нажимаем сохранить
![выбор ДЦ](https://jing.yandex-team.ru/files/cheetah/2021-07-20T12:38:44Z.f9a5da8.png)
5. Копируем название нового хоста
![копируем hostname](https://jing.yandex-team.ru/files/cheetah/2021-07-20T12:40:26Z.519d39f.png)
6. [Добавляем хост в шаблон](https://docs.yandex-team.ru/portal/projects/wboxdb#ishodnyj-kod)

#### Как зайти в консоль MySQL

1. Зайти на хост ```portal-mng2.vla.yp-c.yandex.net``` или ```portal-mng3.sas.yp-c.yandex.net``` по ssh
3. [Выбираем кластер из списка](https://docs.yandex-team.ru/portal/projects/wboxdb#mysql-bazy)
2. Открываем страницу по управлению MySQL кластером и выбираем "Подключиться"
![подключиться](https://jing.yandex-team.ru/files/cheetah/2021-07-20T14:45:08Z.dcd91c1.png)
3. При подключении указываем [пароль от базы](https://docs.yandex-team.ru/portal/projects/wboxdb#paroli-ot-baz)

#### Логи

| Демон | Путь |
|-------|------|
| perl error | /logs/wboxdb/wboxdb.error_log |
| nginx access | /logs/nginx/access.log |
| nginx error | /logs/nginx/error.log |
| haproxy | /logs/haproxy/haproxy-traffic.log |
| juggler | /logs/juggler-checks/ |

#### tcpdump в контейнере

1. Выбираем нужный nanny сервис из [таблички](https://docs.yandex-team.ru/portal/projects/wboxdb#tablica) и заходим в контейнер
2. Вводим команду ```tcpdump -A -i any port 80```
3. Пример запроса за дынными
```
18:22:43.216954 IP6 kmwrvrgwbh3qtfme.sas.yp-c.yandex.net.37132 > stable-wboxdb-ugr-1.sas.yp-c.yandex.net.http: Flags [P.], seq 1:344, ack 1, win 139, options [nop,nop,TS val 3597589683 ecr 1803510248], length 343: HTTP: POST /getpattern?Requestid=1626794563.17473.82559.5065 HTTP/1.1
f....w.9*.........Q.e...*.....8...../......P.oR}.s.5.....q.....
.n..k.a.POST /getpattern?Requestid=1626794563.17473.82559.5065 HTTP/1.1
Accept: */*
Content-Type: application/octet-stream
Host: wboxdb-ugr-int.yandex.net
User-Agent: Yandex WBOX
X-Antirobot-Robotness-Y: 0.0
Connection: Close
Content-Length: 96

.
..........pid
.0....page
.25....block.....palias
.1....project
.21600125....uid
....	container
```

4. Пример ответа от базы

```
18:22:43.226656 IP6 stable-wboxdb-ugr-1.sas.yp-c.yandex.net.http > eb2pswcxbdnr3ln7.sas.yp-c.yandex.net.63108: Flags [P.], seq 1:613, ack 345, win 137, options [nop,nop,TS val 2033217431 ecr 1099073108], length 612: HTTP: HTTP/1.1 200
`......@*.....8...../...*...../;..Q......P..1...........S......
y0o.A..THTTP/1.1 200
Server: nginx/1.12.2
Date: Tue, 20 Jul 2021 15:22:43 GMT
Content-Type: application/octet-stream; charset=ISO-8859-1
Content-Length: 437
Connection: close

.
...........
.1....project
.2018-06-19 16:38:19....updated
.2013-05-05 22:25:45....created
....	container
.538653....pid.....palias
.v12...	prototype
.35489425....uid
.0....temp
.2013-05-06 00:25:45....expires
.1...	protected
.2020-10-12 20:33:20...
lastaccess
.j9PJHZ....salt.........	__WIDGETS
.25....block
.0....page
9layoutType%3D%26fake%3D1%26defskin%3Dbubbles%26pinned%3D1...	psettings....data
.ok....status
.get_pattern....action
```

#### Как посмотреть сколько MySQL хостов доступно в haproxy
1. Подключаемся к контейнеру с использованием local TCP forwarding
```
ssh -L 9000:localhost:9000 <hostname контейнера из nanny> 
```
2. Открываем [админку haproxy](http://localhost:9000/stats)
3. Смотрим готовность к подключению к MySQL базам
![haproxy](https://jing.yandex-team.ru/files/cheetah/2021-07-21T12%3A17%3A22Z.3e7e59d.png)

#### Как выкатывать релиз
1. [Создаем pr](https://docs.yandex-team.ru/portal/projects/wboxdb#ishodnyj-kod), ревьювим, мержим
2. Клонируем последнюю задачу в [sandbox'e](https://docs.yandex-team.ru/portal/projects/wboxdb#sandbox-resursy) и собираем ресурс
![клонируем](https://jing.yandex-team.ru/files/cheetah/2021-07-20T15:50:44Z.40e6503.png)
3. Собираем ресурс
![собираем](https://jing.yandex-team.ru/files/cheetah/2021-07-20T15:51:31Z.3764852.png)
4. Релизим sandbox задачу
![release](https://jing.yandex-team.ru/files/cheetah/2021-07-20T15:57:06Z.ab88413.png)
![release](https://jing.yandex-team.ru/files/cheetah/2021-07-20T15:58:08Z.ea9185e.png)
5. Открываем [дашборд выкладки](https://docs.yandex-team.ru/portal/projects/wboxdb#dashbord-vykladki)
6. Селектим и коммитим
![commit](https://jing.yandex-team.ru/files/cheetah/2021-07-20T15:59:52Z.7f8e977.png)
7. Нажимаем apply
![commit](https://jing.yandex-team.ru/files/cheetah/2021-07-20T16:00:50Z.e28bcab.png)
8. Нажимаем deploy
![deploy](https://jing.yandex-team.ru/files/cheetah/2021-07-20T16:01:54Z.1277daf.png)
9. Еще раз нажимаем deploy
![deploy](https://jing.yandex-team.ru/files/cheetah/2021-07-20T16:03:25Z.16178ee.png)
10. Проверяем правильность ресурсов
11. Если все ок, катим
![катим](https://jing.yandex-team.ru/files/cheetah/2021-07-20T16:04:49Z.b472285.png)
12. Во время релиза смотрим на [графики](https://docs.yandex-team.ru/portal/projects/wboxdb#yasm-paneli) и следим за сообщениями в чате ```Morda Product (monitoring)```

#### Пример грепа пользовательских запросов в mysql
1. Найти запрос пользователя в access логах морды
```
tskv    unixtime=1600200647     timestamp=2020-09-15 23:10:47   timezone=+0300  tskv_format=access-log-morda-ext        ip=2a02:6b8:b080:8014::1:5      x_forwarded_for=2a02:6b8:b080:8014::1:5 method=GET      host=yandex.ru  request=/?from=tabbar   requestid=1600200646.80998.85275.106808 user_agent=Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.86 YaBrowser/20.8.0.893 Yowser/2.5 Safari/537.36     accept_encoding=gzip, deflate, sdch, br accept_language=ru,en;q=0.9,fr;q=0.8,it;q=0.7   bkflags=XXX        content_type=text/html; charset=UTF-8   cookies=yandexuid=72910421493747702; XXX       cryptaid2=14071088974638491243  diff_sid669_vs_uaas=1   enabled-test-buckets=135685,0,92;221195,0,27;278115,0,52        exp=XXX    exp_config_version=15689        fuid_slot=780   geo_h=1 geo_h_age=338   geo_h_loc=55.774181, 37.600601, 140, 1600200309 geo_h_region=213        geo_prec=1      geo_region=213  gpauto_age=338  gpauto_sys=desktop+yabr headers_size=9705       hostname=stable-morda-man-yp-361.man.yp-c.yandex.net    http_version=http2      https=1 icookie=72910421493747702       is_sid669=1     largest_header_size=3973        m_content=big   m_language=ru   m_zone=ru       pid=106808      post=0  protocol=HTTP/1.1       referer=https://yandex.ru/      robotness=0.0   size=247907     status=200      subreq_awaps=1 0 4475 0.056612  subreq_bigb=1 0 18 0.015856     subreq_blackbox=1 0 12707 0.009079        subreq_blender=1 0 31706 0.025723       subreq_business=1 0 111 0.002153        subreq_cacher=1 0 320 0.170176  subreq_cashback_inserts=1 0 20352 0.003774      subreq_direct_firstlook=1 0 2 0.186166  subreq_geohelper_request=1 0 17772 0.025796     subreq_go_backend=1 0 66 0.000744       subreq_personal_request_batch:0=1 0 1510 0.008164       subreq_plus_notification_api=1 0 14 0.004780    subreq_rtbmeta=1 0 11975 0.185614       subreq_topnews=1 0 10171 0.014718       subreq_topnews_user_coldness=1 0 142 0.009541   subreq_video_notif_pers=1 0 23701 0.025608      subreq_weather_ah_forecast_handle=1 0 5981 0.008524 0.0088        subreq_weather_ah_nowcast=1 0 554 0.004703      subreq_yabs=1 0 18145 0.086579  subreq_yalocal_request=1 0 19938 0.094425       subreq_zen_cache_static=1 0 87 0.056422         tcp_rtt=0.009240s       template=v15w   test-bucket=42248,0,42;278115,0,52;273619,0,94;275195,0,44;252937,0,66;252935,0,66;252933,0,66;252655,0,66;221195,0,27;135685,0,92;275069,0,44;272076,0,41;274638,0,76;274329,0,61      timing=total=0.408 pl=0.345 js=0.058 req=0.995 poke=0.009       ua.browserengine=WebKit ua.browserengineversion=537.36  ua.browsername=YandexBrowser    ua.browserversion=20.8.0.893    ua.osfamily=MacOS       ua.osversion=10.12.6    ua.ismobile=0   uid=9964643     uids=505660655,467425953,671711937,683789159,9964643    vhost=www.yandex.ru     wait=5.320      wait_avg=4.328  weather_forecast=request_big_coords     widgets=1       wiha=1  wiha_db=43:9964643:     yandex=1        yandexuid=72910421493747702     yuid_days=1232  yuid_slot_salted=756
```
2. Находим в запросе ```wiha_db=43:9964643:```
```43``` - номер таблицы
```9964643``` - uid
3. [Заходим в консоль mysql](https://docs.yandex-team.ru/portal/projects/wboxdb#kak-zajti-v-konsol-mysql)
4. Находим pid по uid
```
mysql> SELECT * FROM patterns_43 WHERE uid='9964643';
+--------+------+---------+--------+---------+-----------+-----------+------------------------------------------------------------------+------+---------------------+---------------------+-----------+---------------------+---------------------+--------+
| pid    | page | uid     | palias | project | container | protected | psettings                                                        | temp | expires             | created             | prototype | updated             | lastaccess          | salt   |
+--------+------+---------+--------+---------+-----------+-----------+------------------------------------------------------------------+------+---------------------+---------------------+-----------+---------------------+---------------------+--------+
| 813040 |    0 | 9964643 | NULL   |       1 |           |         1 | hidePromo%3D%26pinned%3D1%26columnsCount%3D5%26layoutType%3Drows |    0 | 2015-08-12 21:10:37 | 2015-02-12 21:10:03 | v12       | 2015-02-12 21:10:37 | 2020-09-14 19:43:51 | Sw5e70 |
+--------+------+---------+--------+---------+-----------+-----------+------------------------------------------------------------------+------+---------------------+---------------------+-----------+---------------------+---------------------+--------+
1 row in set (0.00 sec)
```
5. С полученым pid делаем запрос ко всем таблицам
```
mysql> SELECT * FROM patterns_43 WHERE pid='813040'; SELECT * FROM instances_43 WHERE pid='813040'; SELECT * FROM isettings_43 WHERE pid='813040';
+--------+------+---------+--------+---------+-----------+-----------+------------------------------------------------------------------+------+---------------------+---------------------+-----------+---------------------+---------------------+--------+
| pid    | page | uid     | palias | project | container | protected | psettings                                                        | temp | expires             | created             | prototype | updated             | lastaccess          | salt   |
+--------+------+---------+--------+---------+-----------+-----------+------------------------------------------------------------------+------+---------------------+---------------------+-----------+---------------------+---------------------+--------+
| 813040 |    0 | 9964643 | NULL   |       1 |           |         1 | hidePromo%3D%26pinned%3D1%26columnsCount%3D5%26layoutType%3Drows |    0 | 2015-08-12 21:10:37 | 2015-02-12 21:10:03 | v12       | 2015-02-12 21:10:37 | 2020-09-14 19:43:51 | Sw5e70 |
+--------+------+---------+--------+---------+-----------+-----------+------------------------------------------------------------------+------+---------------------+---------------------+-----------+---------------------+---------------------+--------+
1 row in set (0.00 sec)

Empty set (0.00 sec)

+-----+----------+--------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| iid | wid      | pid    | page | isettings                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
+-----+----------+--------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|   1 | _traffic | 813040 |    0 | homeGeo=37.609622%2C55.765564&workLabel=%D0%A0%D0%B0%D0%B1%D0%BE%D1%82%D0%B0&direction=gohome&workId=work&homeLabel=%D0%94%D0%BE%D0%BC&workAddr=%D0%A0%D0%BE%D1%81%D1%81%D0%B8%D1%8F%2C%20%D0%9C%D0%BE%D1%81%D0%BA%D0%B2%D0%B0%2C%20%D1%83%D0%BB%D0%B8%D1%86%D0%B0%20%D0%9B%D1%8C%D0%B2%D0%B0%20%D0%A2%D0%BE%D0%BB%D1%81%D1%82%D0%BE%D0%B3%D0%BE%2C%2016&homeId=home&workGeo=37.587937%2C55.733771&homeAddr=%D0%A0%D0%BE%D1%81%D1%81%D0%B8%D1%8F%2C%20%D0%9C%D0%BE%D1%81%D0%BA%D0%B2%D0%B0%2C%20%D1%83%D0%BB%D0%B8%D1%86%D0%B0%20%D0%91%D0%BE%D0%BB%D1%8C%D1%88%D0%B0%D1%8F%20%D0%94%D0%BC%D0%B8%D1%82%D1%80%D0%BE%D0%B2%D0%BA%D0%B0%2C%2021%2F7%D1%812 |
+-----+----------+--------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```
# Действия при поломках

## Как понять что есть проблема

Продуктово может не работать:
 - настройка города погоды
 - настройка котировок
 - настройка любимой рубрики новостей

При полной недоступности баз пользователи увидят красный баннер вверху главной страницы
![баннер](https://jing.yandex-team.ru/files/cheetah/Снимок%20экрана%202021-02-10%20в%2017.18.27.png)

## Как локализовать проблему

**Проблема возможно большая** - оповестить руководителя, действовать по плану ниже.
**Проблема очевидно небольшая** - начать отсчет 15 минут и действовать по плану ниже.

1. Проверить чаты
    - [факапочная](https://t.me/joinchat/BlyRekEwILp56Vu030x2gg)
    - [мониторинг продукта](https://t.me/joinchat/BlyRegsiusIHkvRRW8y7Ug)
    - [MDB Emergency](https://t.me/c/1088650226/124421)
    - [координация больших факапов](https://t.me/joinchat/BeUD0kQlNiNqon4C7SSIlQ)
    - [покатушки](https://t.me/joinchat/BlyRek7XrnZIJpDaD8C3kQ)
2. [Проверить основные графики](https://docs.yandex-team.ru/portal/projects/wboxdb#yasm-paneli)
3. [Проверить графики awacs балансеров](https://docs.yandex-team.ru/portal/projects/wboxdb#tablica)
4. [Проверить алерты](https://juggler.yandex-team.ru/dashboards/49570ecf)
5. [Просмотреть события в infra](https://infra.yandex-team.ru)

Если в течение 15 минут проблема не локализована, оповестить руководителя. Дальше решение принимает руководитель.
**Если нет руководителя звонить кому угодно:** wwax@ dkhlynin@ merzavcev@ nufina@

## Как потушить

Тут все зависит от характера проблемы. Согласно [схеме](https://a.yandex-team.ru/arc_vcs/portal/docs/projects/wboxdb.md?edit=true#shema) определить уровень, на котором произошла поломка.
1. **Уровень MDB**. MySQL базы не отвечают или нет мастера, запросы выполняются медленно
    - координация в чате [MDB Emergency](https://t.me/c/1088650226/124421)
2. **Уровень Nanny**. Проблемы с контейнерами или работой кода, демонов.
    - координация в чате **True Котаны**(закрытый чат, добавляет руководитель)
3. **Уровень L3 + AWACS**. Проблемы с доступностью балансера, фейлы при подзапросах.
    - координация в чате **True Котаны**(закрытый чат, добавляет руководитель)
    - координация в чате [L7-balancer-emergency](https://t.me/joinchat/Cbhulkz_7ZPg6vJdCrcMpg)
4. **Уроверь бекенда морды**. Ошибки при подзапросах с морды, ошибки при обработки ответа от баз.
    - координация в чате [покатушки](https://t.me/joinchat/BlyRek7XrnZIJpDaD8C3kQ)
