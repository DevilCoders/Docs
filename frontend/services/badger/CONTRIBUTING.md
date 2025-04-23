# Быстрый старт

```
npm run dev
```

Некоторые сервисы доступы только через token, для этого нужно его получить и положить в окружение. В сервисе поддерживается файл .env.

Токены:
- **OKO_OAUTH_TOKEN**: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=d1d20b275ba44762ad26cb8c1e357cff
- **STARTREK_OAUTH_TOKEN**: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b

Если у вас есть доступ к нужным ключам в секретнице, воспользуйтесь командой `npm run env`, для создания .env файла. 

## Debug

Debug github: ```DEBUG=octokit:rest*``` or ```DEBUG=badger:github*```

Debug npm: ```DEBUG=npm```

Debug oko: ```DEBUG=oko```

# Инфраструктура:

## Production

**Url**: https://badger.yandex-team.ru<br />
**Source**: stable<br />
**Deploy**: [badger-production](https://deploy.yandex-team.ru/stages/badger-production)<br />
**Nanny**:
  [badger-production-backend](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/backends/list/deploy-badger-production/),
  [badger-production-upstream](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/upstreams/list/badger-production-upstream/),
  domain [prod](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/domains/list/prod/show/),
  cert [badger.yandex-team.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/certs/list/badger.yandex-team.ru/)
**DC**: MYT, SAS, VLA

## Development

**Url**: https://trunk.test.badger.yandex-team.ru<br />
**Source**: master/trunk branch (last changes)<br />
**Deploy**: [badger-trunk](https://deploy.yandex-team.ru/stages/badger-trunk)<br />
**Nanny**:
  [badger-testing-backend](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/backends/list/deploy-badger-testing/),
  [badger-testing-upstream](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/upstreams/list/badger-testing-upstream/),
  domain [trunk](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/domains/list/trunk/show/),
  cert [test.badger.yandex-team.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/certs/list/test.badger.yandex-team.ru/)
**DC**: only SAS

## Next release

**Url**: https://release.test.badger.yandex-team.ru<br />
**Source**: release branch<br />
**Deploy**: [badger-release](https://deploy.yandex-team.ru/stages/badger-release)<br />
**Nanny**:
  [badger-release-backend](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/backends/list/deploy-badger-release/),
  [badger-release-upstream](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/upstreams/list/badger-release-upstream/),
  domain [release](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/domains/list/release/show/),
  cert [all_subdomains.test.badger.yandex-team.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/certs/list/all_subdomains.test.badger.yandex-team.ru/)
**DC**: only MYT

## Betas

**Url**: https://pr-12345.test.badger.yandex-team.ru<br />
**Source**: pull-requests<br />
**Deploy**: [pr-NNNNNN](https://deploy.yandex-team.ru/projects/badger)<br />
**Nanny**:
  dynamic backend [pull-NNNNNN-backend](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/backends/list/),
  dynamic upstream [pull-NNNNNN-upstream](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/upstreams/list/),
  dynamic domain [pull-NNNNNN-domain](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/show/),
  cert [all_subdomains.test.badger.yandex-team.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/badger.yandex-team.ru/certs/list/all_subdomains.test.badger.yandex-team.ru/)
**DC**: only MYT
