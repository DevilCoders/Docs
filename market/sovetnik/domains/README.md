# Getting started

## Install
```bash
git clone git@github.yandex-team.ru:sovetnik/sovetnik-domains.git
```

## Build
```bash
make build
```

## How to start?

### Development

#### Environment

It's necessary to add `.env` file to root of the project:
```yaml
TVM_SECRET=

Q_OAUTH_ACCESS_TOKEN=
YT_OAUTH_ACCESS_TOKEN=
TVM_OAUTH_ACCESS_TOKEN=tvmtool-development-access-token
WIKI_OAUTH_ACCESS_TOKEN=
SLACK_OAUTH_ACCESS_TOKEN=
STAFF_OAUTH_ACCESS_TOKEN=
TRACKER_OAUTH_ACCESS_TOKEN=
GITHUB_OAUTH_ACCESS_TOKEN=

BITBUCKET_USERNAME=robot-sovetnik
BITBUCKET_PASSWORD=

REDIS_HOST=127.0.0.1
REDIS_PORT=6379
```

```bash
docker-compose up --detach
node -r dotenv/config ./build/server.js
node -r dotenv/config ./build/background.js
```

### Production

#### Environment

It's necessary to add `.env` file to root of the project:
```yaml
TVM_SECRET=

Q_OAUTH_ACCESS_TOKEN=
YT_OAUTH_ACCESS_TOKEN=
TVM_OAUTH_ACCESS_TOKEN=
WIKI_OAUTH_ACCESS_TOKEN=
SLACK_OAUTH_ACCESS_TOKEN=
STAFF_OAUTH_ACCESS_TOKEN=
TRACKER_OAUTH_ACCESS_TOKEN=
GITHUB_OAUTH_ACCESS_TOKEN=

BITBUCKET_USERNAME=robot-sovetnik
BITBUCKET_PASSWORD=

REDIS_MASTER_SET=
REDIS_MASTER_PASSWORD=
REDIS_SENTINEL_HOST=
REDIS_SENTINEL_PORT_NUMBER=
```

```bash
export NODE_ENV=production && ./scripts/run.sh --workers count -pwd path --log-dir path --interpreter /opt/nodejs/10/bin/node
```

# Scripts

- [`./scripts/run.sh -- utility to run a service`](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/Scripts#runsh)
- [`./scripts/loadbalancer.sh -- utility to trigger a load balancer action`](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/Scripts#loadbalancersh)

# API

## Reports

### [Get information about reports](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#get-information-about-reports)
```
GET /api/v1/reports
```

#### Query parameters

| Name                 | Type     | Description                                                                           |
| -------------------- |:--------:|:------------------------------------------------------------------------------------- |
| `status`             | `string` | **Required**. Either `OPEN`, `PROCESSING`, `RESOLVED` or `CLOSED` to filter by status |
| `staff`              | `string` | The staff login of a selectorman                                                      |
| `count`              | `number` | The number of items that will be returned. Default: `10000`                           |
| `priority`           | `number` | The priority of items that will be returned                                           |
| `priority_less_than` | `number` | Sets the upper bound of the priorities of target items                                |
| `priority_more_than` | `number` | Sets the lower bound of the priorities of target items                                |

### [Get information about report](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#get-information-about-report)
```
GET /api/v1/reports/:report
```

#### Query parameters

| Name     | Type     | Description           |
| -------- |:--------:|:--------------------- |
| `report` | `string` | **Required**. The report's identity |

### [Create reports](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#create-reports)
```
POST /api/v1/reports
```

#### Body parameters
| Name       | Type       | Description                                |
| ---------- |:----------:|:------------------------------------------ |
| `url`      | `string`   | **Required**. The url of the website       |
| `priority` | `number`   | The priority. Default: `current timestamp` |
| `broken`   | `string[]` | The list of broken fields. Default: `[]`   |

### [Assign reports](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#assign-reports)
```
POST /api/v1/reports/assign
```

#### Query parameters
| Name         | Type      | Description                                                |
| ------------ |:---------:|:---------------------------------------------------------- |
| `staff`      | `string`  | **Required**. The staff login of a selectorman             |
| `count`      | `number`  | The number of items that will be assigned. Default: `10`   |
| `restricted` | `boolean` | Do assigned reports have restricted type? Default: `false` |

### [Assign a report](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#assign-report)
```
POST /api/v1/reports/:id/assign
```

#### Query parameters
| Name     | Type     | Description                                               |
| -------- |:--------:|:--------------------------------------------------------- |
| `staff`  | `string` | **Required**. The staff login of a selectorman            |

### [Accept reports](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#accept-reports)
```
POST /api/v1/reports/accept
```

#### Query parameters
| Name     | Type     | Description                                               |
| -------- |:--------:|:--------------------------------------------------------- |
| `staff`  | `string` | **Required**. The staff login of a selectorman            |
| `count`  | `number` | The number of items that will be accepted. Default: `500` |

### [Accept a report](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#accept-report)
```
POST /api/v1/reports/:id/accept
```

### [Approve reports](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#approve-reports)
```
POST /api/v1/reports/approve
```

#### Query parameters
| Name    | Type       | Description                                               |
| ------- |:----------:|:--------------------------------------------------------- |
| `ids`   | `string[]` | The array of id of the reports                            |
| `urls`  | `string[]` | The array of url of the websites                          |
| `count` | `number`   | The number of items that will be accepted. Default: `500` |

#### Examples
```
POST /api/v1/reports/approve?urls[]=wildberries.ru&urls[]=eldorado.ru
```

```
POST /api/v1/reports/approve?ids[]=052c19c7-ce14-4a18-937c-adebd1084bb3&ids[]=0586c1f5-8d48-4da4-9b64-13319c498319
```

### [Approve a report](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#approve-report)
```
POST /api/v1/reports/:id/approve
```

## Domains

### [Get information about domains](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#get-information-about-domains)
```
GET /api/v1/domains
```

#### Query parameters
| Name   | Type       | Description                                                |
| ------ |:----------:|:---------------------------------------------------------- |
| `urls` | `string[]` | The NOT EMPTY array of url of the websites                           |

### [Get information about domain](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#get-information-about-domain)
```
GET /api/v1/domains/:domain
```

#### Query parameters

| Name     | Type     | Description               |
| -------- |:--------:|:------------------------- |
| `domain` | `string` | **Required**. Domain name |

### [Add rules to domains](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#update-information-about-domain)
```
POST /api/v1/domains/rules
```
- add passed rules. (if not presents)
- not existing domains will be created with passed rules

#### Body parameters
| Name         | Type       | Description                                    |
| ------------ |:----------:|:---------------------------------------------- |
| `urls`       | `string[]` | **Required**. not empty array with domains     |
| `rules`      | `string[]` | **Required**. not empty array with rules       |


### [Update information about domain](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#update-information-about-domain)
```
POST /api/v1/domains/:domain
```

#### Query parameters

| Name     | Type     | Description               |
| -------- |:--------:|:------------------------- |
| `domain` | `string` | **Required**. Domain name |

#### Body parameters
| Name         | Type       | Description                                    |
| ------------ |:----------:|:---------------------------------------------- |
| `type`       | `string`   | The type of the domain. Default: `shop`        |
| `status`     | `string`   | The status of the domain. Default: `failed`    |
| `restricted` | `boolean`  | The restricted flag. Default: `false`          |
| `payload`    | `object`   | The new payload of the domain. Default: `ToDo` |
| `rules`      | `string[]` | The list of rules. Default: `[]`               |
| `comments`   | `string[]` | The list of comments. Default: `[]`            |

### [Remove domain](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#remove-domain)
```
DELETE /api/v1/domains/:domain
```

#### Query parameters

| Name     | Type     | Description               |
| -------- |:--------:|:------------------------- |
| `domain` | `string` | **Required**. Domain name |


### Generates and send payment acts via Q
```
POST /api/v1/selectormen/:staff/acts
```


#### Query parameters

| Name     | Type     | Description               |
| -------- |:--------:|:------------------------- |
| `staff`  | `string` | **Required**. staff name |

## Balancers

### [Ping](https://github.yandex-team.ru/sovetnik/sovetnik-domains/wiki/API#ping)
```http
GET /ping
```

## Clone DB into local machine

1. Install Postgresql:
    `brew install postgresql`
2. Create dump from server:
    - `pg_dump -h <host> -p <port> -U <user> -F c -f ./dump.tar.gz <db_name>`
        > `pg_dump -h c-mdb7jbpb3v22voemo0mi.rw.db.yandex.net -p 6432 -U sovetnikdomains -F c -f ./dump.tar.gz sovetnikdomains_db`
3. Create own database:
    - `psql postgres`
    - `CREATE DATABASE sovetnikdomains_db;`
    - `exit`
4. Read user:
    - `psql postgres`
    - `select usename, passwd from pg_shadow;`
    - `exit`
5. Import dump:
    - `pg_restore -h localhost -p <port> -U <username> -F c -d <db_name> ./dump.tar.gz`
        > `pg_restore -h localhost -p 5432 -U timsv -F c -d sovetnikdomains_db ./dump.tar.gz`
