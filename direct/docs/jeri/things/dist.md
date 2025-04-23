# dist

`dist.yandex.ru` — это Яндексовый сервис для хранения deb-пакетов.

Сущности:

- репозиторий, например `direct-trusty`
- внутри репозитория ветки, обычно `unstable`, `testing`, `stable`
- внутри веток лежат пакеты, у каждогого пакета может быть много версий


Как увидеть репозитории:

```
ssh dupload.dist.yandex.ru ls /repo
```

Как поискать пакет, утилита Директовская, работает с `ppcdev`

```
$ dt-dist find yandex-direct-dna |grep 0.312
| direct-trusty | testing   | yandex-direct-dna_0.312.0_all.deb                            |
| direct-trusty | testing   | yandex-direct-dna_0.312.0_amd64.changes                      |
| direct-trusty | testing   | yandex-direct-dna_0.312.0.tar.gz                             |
| direct-trusty | testing   | yandex-direct-dna_0.312.0.dsc                                |
| direct-trusty | stable    | yandex-direct-dna_0.312.0-1-g19da43728d_all.deb              |
| direct-trusty | stable    | yandex-direct-dna_0.312.0-1-g19da43728d_amd64.changes        |
| direct-trusty | stable    | yandex-direct-dna_0.312.0-1-g19da43728d.tar.gz               |
| direct-trusty | stable    | yandex-direct-dna_0.312.0-1-g19da43728d.dsc                  |
```

Здесь:
- `direct-trusty` — репозиторий,
- `testing` и `stable` — ветки,
- `yandex-direct-dna` — имя пакета,
- `0.312.0` и `0.312.0-1-g19da43728d` — версии.

Полезные команды: `dupload`, `dt-dist`, `apt`

Полезные ссылки:

- Инструкция: [{#T}](../../guide/dev/how-to-package.md)
- Сервис в abc: <https://abc.yandex-team.ru/services/DIST>


