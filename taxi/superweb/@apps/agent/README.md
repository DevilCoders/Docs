# Support Agent Frontend

## [Wiki](https://wiki.yandex-team.ru/taxi/partnerproducts/frontend/projects/agent/)

## Development

### Starting local dev server

To start working with project you should have [mkcert](https://github.com/FiloSottile/mkcert) installed

```bash
brew install mkcert
mkcert -install
```

Also you should have `0.0.0.0 agent.localhost.yandex-team.ru` in your `/etc/hosts`

Install dependencies, generate certificate and start dev server

```bash
yarn
cd @apps/agent
yarn mkcert
yarn dev
```

### Pushing i18n messages

Get your OAUTH_TOKEN at https://nda.ya.ru/3SjQY7 and set is as an environment variable in `@apps/agent/.env.local`

```sh
OAUTH_TOKEN=...
```

Then you can push default messages

```sh
yarn intl-push
```
