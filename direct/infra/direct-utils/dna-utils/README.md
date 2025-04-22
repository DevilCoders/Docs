# DNA Utils

различные утилиты для DNA

доступные команды:

`tests` - запуск интеграционных тестов DNA в сэндбоксе (`dna-utils tests --help`)

`rerun-failed` - перезапуск упавших интеграционных тестов DNA из таски в сэндбоксе (`dna-utils rerun-failed --help`)

`get-latest-release-num` - вывести номер текущего релиза (в формате `0.233.0`)

`get-latest-release-package` - вывести версию пакета текущего релиза (в формате `0.232.0-1-g9c89dbef41`)

`get-latest-release-key` - вывести startrek-тикет текущего релиза (в формате `DIRECT-120874`)

`update-omnipotent-betas` - обновить единые беты для автотестов DNA

## Сборка пакета

для сборки используется утилита [ya tool](https://wiki.yandex-team.ru/yatool/)

для deb-пакета потребуется gpg-ключ

```bash
`arc root`/ya package --debian --publish-to direct-trusty pkg.json
```

для обновления пакета
```bash
direct-test-update ppcdev-all yandex-du-dna-utils=$VERSION
```
