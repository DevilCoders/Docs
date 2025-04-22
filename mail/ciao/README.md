# ciao

### Разработка
1. Поднять мегаманид
    * На дев-виртуалке монтируем `arc`
    * `ya make --build=debug --sanitize=address --force-build-depends --checkout alice/megamind/scripts/run`. Ест много памяти, OOM может прибить arc.
    * В `alice/megamind/configs/dev/scenarios/mail_ciao.pb.txt` прописываем `BaseUrl: "http://localhost:8001/megamind/"`, `Tvm2ClientId: "2018344"`, `Enabled: True`
    * Запрашиваем роль в https://abc.yandex-team.ru/services/bassdevelopers/, чтобы при запуске был доступ к секретам
    * Запуск: `alice/megamind/scripts/run/run -p 7007 -c alice/megamind/configs/dev/megamind.pb.txt`
2. Запускаем тунель до вируталки: `make tunnel`
3. Запускаем CIAO:
    * `make build_bin`
    * `make update-po && make build-mo && make CIAO_MO_USE_LOCAL=True runserver`
4. Настраиваем клиент:
    * Прописываем адрес мегамаинда https://wiki.yandex-team.ru/alice/megamind/protocolscenarios/otladka-v-prilozhenii/
    * Прописываем флаги экспериментов https://wiki.yandex-team.ru/mail/swat/ciao/podkljuchenie-navyka-dlja-testirovanija/
5. Не забываем перед запуском сервера сформировать конфиг `ciao` в `tvmtool`

### QA
Чтобы обратиться к навыку на QA, нужно:
1. Выставить Vins URL равный http://megamind-ci.alice.yandex.net/speechkit/app/pa/

### Литература
https://wiki.yandex-team.ru/alice/megamind/#kakzapuskat
https://wiki.yandex-team.ru/alice/megamind/protocolscenarios/otladka-v-prilozhenii/
https://wiki.yandex-team.ru/alice/megamind/protocolscenarios/
https://wiki.yandex-team.ru/mail/swat/ciao/podkljuchenie-navyka-dlja-testirovanija/
https://a.yandex-team.ru/arc/trunk/arcadia/alice/megamind/configs/dev/scenarios/mail_ciao.pb.txt

### TVM
Чтобы добавить запуск tvmtool нужно:
1. Положить в `.tvm.key` секрет.
2. В `run_local.sh` прописать `self_tvm_id`.
Между перезапусками нужно самостоятельно удалять `.tvm.json`, если была ошибка запуска tvmtool.
