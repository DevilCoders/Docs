Пакет для мониторинга корок и отправки трейсов в [сервис автоматической агрегации корок](https://coredumps.n.yandex-team.ru). Работает на гипервизоре. Мониторит корки при падениях в контейнере.

### Собрать
Для сборки необходимо завести GPG ключ (см. [инструкцию](https://wiki.yandex-team.ru/geotargeting/products/ipreg/utils/pkgsign/>)).
Узнать id ключа можно с помощью команды `gpg -K`, в выводе `XXXXXXXX` - это и будет id ключа.

```
$ gpg -K
/home/<login>/.gnupg/secring.gpg
----------------------------------
sec   2048R/XXXXXXXX 2020-07-22
uid                  Name <login@yandex-team.ru>
```

Чтобы пакет мог поставиться на старых машинах, нужно сменить сжатие с дефолтного xz на gzip.
```
$ ya package --debian --debian-compression-type gzip --key AAAHEREG pkg.json
```

Собирается архив `yandex-market-corewatcher-rtc.1.3997672.tar.gz` Надо распаковать:
```
$ tar -zxf yandex-market-corewatcher-rtc.1.3997672.tar.gz
```

### Выложить в dist
Настроить dupload: <https://wiki.yandex-team.ru/direct/moderate/dist.yandex.ru/>

Конфиг dupload.conf взять отсюда: <https://wiki.yandex-team.ru/market/development/newdeveloper/>

```
$ dupload --to common yandex-market-corewatcher-rtc_1.3997672_amd64.changes
```

### dmove в stable
Зайти на `dupload.dist.yandex.ru` по ssh и сделать `dmove` из unstable в stable

```
$ sudo dmove common stable yandex-market-corewatcher-rtc 1.3997672 unstable
```

Если тебя не пускает - просишь дежурного. Если ты сам дежурный - просишь добрых людей из [группы](https://golem.yandex-team.ru/usergroup.sbml?usergroup=svc_dist_administration) либо [запрашиваешь права](https://wiki.yandex-team.ru/runtime-cloud/services/dist/#pravanarmove/dmove/bmove).

### Обновляем версии в salt
В [репозитории](https://bb.yandex-team.ru/projects/RTCSALT/repos/market/browse/) в файле `units.d/market-base.yaml` нужно обновить версию библиотеки, а так же апнуть версию в поле `meta.version`.

Изменения следует вносить в форк репозитория, пулл реквест в ветку prestable можно сделать через интерфейс. Далее необходимо [поставить задачу](https://st.yandex-team.ru/createTicket?queue=CSADMIN&priority=2&summary=%D0%92%D1%8B%D0%BA%D0%B0%D1%82%D0%B8%D1%82%D1%8C+%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D1%8E+hostman&tags%5B%5D=cs_duty&type=2) в CSADMIN с указанием пулл реквеста.

Следить за раскладкой пакета `market-base` можно [здесь](http://hm-sas.in.yandex.net/units/market-base).
