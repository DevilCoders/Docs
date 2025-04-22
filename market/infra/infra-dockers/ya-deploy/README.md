haproxy для графита / графауса находится в yandex deploy [один из боксов]
тестинг: https://yd.yandex-team.ru/stages/market-infra_market-graphite_testing

Чтобы его запустить, необходимо создать / обновить по необходимости ресурсы в сендбоксе,
которые используются как слои в deploy unit, и накладываются на файловую систему.


ya upload --ttl=inf --tar -d "config, readme: https://github.yandex-team.ru/market-infra/infra-dockers/blob/master/ya-deploy/README.md" haproxy/config/*

ya upload --ttl=inf --tar -d "run-script, readme: https://github.yandex-team.ru/market-infra/infra-dockers/blob/master/ya-deploy/README.md" haproxy/run-script/*

###### path to ya : e.q. /Users/${USER}/arc/arcadia/ya