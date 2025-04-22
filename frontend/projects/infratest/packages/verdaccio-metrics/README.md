# @yandex-int/verdaccio-metrics

Add unistat into verdaccio

## Run with docker

```bash
cd ~/infratest/packages/verdaccio-metrics
curl 'https://proxy.sandbox.yandex-team.ru/1610367887/.npmusers' > config/.npmusers
docker-compose up
```

`verdaccio-yandex-metrics` будет использоваться из текущего каталога, поэтому может потребоваться выполнить `npm run build`.

Необходимо, чтобы в окружении были доступны `AWS_ACCESS_KEY_ID` и `AWS_SECRET_ACCESS_KEY`.
[Как получить ключи от AWS](https://wiki.yandex-team.ru/search-interfaces/infra/report-renderer/kb/#i).
В свои dotfiles добавляйте переменные с `export` – иначе они не будут прокинуты.
