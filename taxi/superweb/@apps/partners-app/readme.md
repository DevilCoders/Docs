# Partners applications

## Getting started

All actions are executed in the project folder `@apps/partners-app/`

Installing node modules

```
yarn install
```

Installing mkcert (if not installed)

```
brew install mkcert
```

Generating certificates

```
yarn mkcert
```

Make certificates to be trusted automatically:

```
mkcert -install
```

At the `hosts` file, add the route to the project

Open `hosts` file to edit

```
sudo nano /etc/hosts
```

Add the following line

```
0.0.0.0         partners-app.localhost.yandex.ru
```

Result (example)

```
...
127.0.0.1       localhost
255.255.255.255 broadcasthost
::1             localhost
0.0.0.0         partners-app.localhost.yandex.ru
```

Save the `hosts` file

And just run the project

```
yarn dev
```

The project is available locally via the [link](https://partners-app.localhost.yandex.ru/)
Credentials and accounts are [here](https://yav.yandex-team.ru/secret/sec-01ff2cwjb0ct20a43gdkkhqy5t/explore/version/ver-01g3bfajy8bd1nwv7gq2gy9w46)
