# @yandex-fleet/signalq-fw-setup

## Development

Clone the repo

```shell
git clone https://github.yandex-team.ru/taxi/fleet-web
cd fleet-web
```

Install `Node.js` version with [nvm](https://github.com/nvm-sh/nvm)

```shell
nvm install
```

Install Yarn binary globally

```shell
npm i -g yarn
```

Install dependencies

```shell
yarn
```

Default [environment variable](#environment-variables) values are stored in `.env`.
To override defaults locally [use `.env.local`](https://create-react-app.dev/docs/adding-custom-environment-variables/#adding-development-environment-variables-in-env)

Run the development server

```shell
yarn signalq-fw-setup:start
```

By default, the development server will be launched on port 3000.
Open http://localhost:3000 to view the app in the browser.

## Environment variables

| Name         | Description                                                                                                                                                                                                                                                                                                                                        |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| MOCK_DATA    | If set to `true`, mock data should be returned in camera API responses where possible. Settings this variable may be useful when you want to start your dev server without having an ability to proxy requests to the real camera and still be able to view the app in the browser like when the camera is online.                                 |
| PROXY_TARGET | If set, all camera API requests will be proxied to that target. For example, if `PROXY_TARGET` is set to `192.168.0.1`, the request with URL `http://localhost:3000/cgi-bin/foo` will be proxied to `http://192.168.0.1/cgi-bin/foo`. Setting this variable may be useful when you want to proxy requests from your dev server to the real camera. |
