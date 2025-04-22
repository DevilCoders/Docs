# Backend

## Requirements

- [nvm](https://github.com/creationix/nvm)
- node (see version in [.nvmrc](.nvmrc))

## Setup

```sh
nvm use && npm i --registry=https://npm.yandex-team.ru
```

## Development

.env
```dotenv
# sovetnik-market-internal-key
MARKET_INTERNAL_KEY=
# sovetnik-market-partner-key
MARKET_PARTNER_KEY=
NODE_ENV=development
MONGODB_PASS=
YT_OAUTH_ACCESS_TOKEN=
REDIS_PASS=
TVM_OAUTH_ACCESS_TOKEN=tvmtool-development-access-token
TVM_SERVER_URL=http://localhost:8001
```

Run tvmtool, .tvm.json is required

```json
{
  "BbEnvType": 2,
  "clients": {
    "sovetnik-backend-local": {
      "self_tvm_id": "[ASK FOR tvm_id]",
      "secret": "[ASK FOR tvm secret]",
      "dsts": {
        "blackbox": {
          "dst_id": 223
        },
        "bigb": {
          "dst_id": 2001337
        },
        "social": {
          "dst_id": 2000381
        }
      }
    }
  },
  "port": 13013
}
```

```sh
npm run start:tvm
```

```sh
npm start
```
