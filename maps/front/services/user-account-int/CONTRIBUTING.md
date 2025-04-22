# Contributing

## Requirements

The project is build on [Node.js](http://nodejs.org/) application engine and uses [npm](http://npmjs.org) for tracking dependencies.
It is highly recommended to develop using the same versions of `node` and `npm` as in the [baseimage](Dockerfile#L1).
For switching quickly between Node.js version you can use a Node.js version manager such as [n](https://github.com/tj/n).

## Getting Started

1. Go to the service folder in Arcadia

   ```sh
   cd /maps/front/services/user-account-int
   ```

2. Switch to needed Node.js version from `.nvmrc` file:

   ```sh
   nvm use
   ```

3. Install dependencies:

   ```sh
   npm ci
   ```

4. Build and run the service in development mode:

   ```sh
   make dev
   ```

By default http-service starts listening on port `8080`. If you started the application locally it should respond on:
```
http://localhost:8080/v1/stub_endpoint
```

To change the port on which the application listens change the `MAPS_NODEJS_PORT` environment variable:

```
MAPS_NODEJS_PORT=8666 make dev
```

## TVM tickets

For development, you must use tvm tickets. For ability to generate it, follow steps below:

1. Download tvmknife using this [instruction](https://wiki.yandex-team.ru/passport/tvm2/debug/#tvmknife)
2. Sign up in https://passport-test.yandex.ru and then sign in.
3. Get **Session_id** from Cookies: `3:1573 ...`
4. Generate USER_TICKET:  
**IMPORTANT:** You must add "TVM ssh пользователь" role in ABC service.
```bash
# ./ya tool tvmknife get_user_ticket sessionid --tvm_id <self_tvm_id> -s '<Session_id>' -h '<host>' -b <BB_host> -u '<user_ip>' --ssh_login '<login_from_staff>'
$ ./ya tool tvmknife get_user_ticket sessionid --tvm_id 2015745 -s '3:1573 ...' -h 'yandex.ru' -b blackbox-test.yandex.net -u '<user_ip>' --ssh_login '<login_from_staff>'
```
5. Generate SERVICE_TICKET:
```bash
# ./ya tool tvmknife get_service_ticket client_credentials -s <self_tvm_id> -d <self_tvm_id> -S <secret>
./ya tool tvmknife get_service_ticket client_credentials -s 2015745 -d 2015745 -S VOKRqKM6OjiY0RbOT6eIZw
```

## Testing

For run all tests use the command:

```
make validate
```

## Manual testing in mobile yandex maps

If you want to test the service in mobile yandex maps, you should change provider:
```
Settings -> Debug panel -> Environment -> Mobmaps proxy host -> testing
```

## Deploying

### Release to testing
This project uses [qtools](https://github.yandex-team.ru/maps/infra/tree/master/packages/qtools)
(`qtools` for short) to interface with docker, the docker registry and the cloud platform Deploy.

```sh
make patch # or minor, major
arc pr create --push --publish --no-edit
```

Merge new PR after all checks. Pull trunk. Then create tag locally and push it to tags/releases:
```sh
make arc-tag
arc push <tag_name>:tags/releases/maps-front/user-account-int/<tag_name>
```

The new arc tag will trigger a CI (Trendbox) build which:

1. Run tests.
2. Builds a docker image.
3. Pushes it to registry.
4. Deploys it to testing.

### Deploy the current version to production

```
npx qtools deploy production
```

## Style Guides

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)
