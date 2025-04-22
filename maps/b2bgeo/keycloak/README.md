# Keycloak service

[Documentation](https://www.keycloak.org/)

## Admin Credentials

- [stable](https://yav.yandex-team.ru/secret/sec-01g1qx6ww4yd9hnwzg41pts4px)
- [testing](https://yav.yandex-team.ru/secret/sec-01g4hrjgwwzvg5sn9pgbzh1b0s)

## Service
[Docker repo](https://us-east-2.console.aws.amazon.com/ecr/repositories/private/582601430203/keycloak?region=us-east-2)

## Database

RDS cluster:

| Staging | Credentials | DN Name |
| ------- | ----------- | ------- |
| [stable](https://us-east-2.console.aws.amazon.com/rds/home?region=us-east-2#database:id=keycloak-postgres;is-cluster=false) | [b2bgeo-aws-keycloak-postgres-user](https://us-east-2.console.aws.amazon.com/secretsmanager/home?region=us-east-2#!/secret?name=stable%2Fkeycloak%2Fpostgres) | keycloak-db |
| [testing](https://us-east-2.console.aws.amazon.com/rds/home?region=us-east-2#database:id=keycloak-testing-postgres;is-cluster=false) | [b2bgeo-aws-keycloak-testing-postgres-user](https://us-east-2.console.aws.amazon.com/secretsmanager/home?region=us-east-2#!/secret?name=testing%2Fkeycloak%2Fpostgres) | keycloak-db-testing |

## How to deploy a new service

Create a temporary development Ubuntu VM inside an AWS cluster. This VM is only needed to interact with services inside AWS (because it's impossible to access them from the outside). Connect to it using SSH, e.g.:

```bash
# Following IP address is fake (given only as an example)
ssh -i aws-vm.pem ubuntu@192.0.2.42
```

### Database creation

Install postgresql client:

```bash
sudo apt install postgresql-client-12
```

Connect to the database (see [docs](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ConnectToPostgreSQLInstance.html)):

```bash
psql \
   --host=keycloak-postgres.c8ui3xlnkxhc.us-east-2.rds.amazonaws.com \
   --port=5432 \
   --username=keycloak_user \
   --password \
   --dbname=postgres
```

Create Keycloak DB:

```sql
CREATE DATABASE "keycloak-db";
```

### Admin user creation

Install java:

```bash
sudo apt update && sudo apt install openjdk-11-jre
java --version
```

Generate admin password:

```bash
openssl rand -base64 64 | tr -d '\n\r' ; echo ''
```

Save it to Vault.

Download keycloak on the VM as a tarball from the official website and unpack it.
Start `kc.sh` (**put a space** before the command to prevent it from saving to shell history along with all credentials).
Use DB password from AWS Secrets Manager and the admin user password generated previously.

```bash
 KC_DB="postgres" \
KC_DB_URL="jdbc:postgresql://keycloak-postgres.c8ui3xlnkxhc.us-east-2.rds.amazonaws.com:5432/keycloak-db" \
KC_DB_USERNAME="keycloak_user" \
KC_DB_SCHEMA="public" \
KC_HOSTNAME="auth.routeq.com" \
KC_DB_PASSWORD=*** \
KEYCLOAK_ADMIN=admin \
KEYCLOAK_ADMIN_PASSWORD=*** \
 ./kc.sh start-dev \
  --log-level INFO
```

Pay attention to the console output and check that _master realm_ and _user 'admin'_ are created successfully:

```
...
2022-04-28 11:04:30,451 INFO  [org.keycloak.services] (main) KC-SERVICES0050: Initializing master realm
2022-04-28 11:04:34,912 INFO  [org.keycloak.services] (main) KC-SERVICES0009: Added user 'admin' to realm 'master'
...
2022-04-28 11:04:35,096 WARN  [org.keycloak.quarkus.runtime.KeycloakMain] (main) Running the server in development mode. DO NOT use this configuration in production.
```

If everything goes OK, stop the process.

