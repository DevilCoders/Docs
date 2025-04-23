# Intro

[In russian](./intro.md)

# Installation

```bash
npm ci
cd server
npm ci
cd ..
```

## mac os

Add the following to `/private/etc/hosts`

```
127.0.0.1       localhost.yandex-team.ru
```

## windows

Add the following to `C:\Windows\System32\drivers\etc`

```
127.0.0.1       localhost.yandex-team.ru
```

# Usage

```
// in the first tab
npm run start

// in the second tab
npm run dev:server
```

### Run only client

```
npm run start:only-client
```

Open https://localhost.yandex-team.ru:8080

# Deploy

https://deploy.yandex-team.ru/projects/modadvert-supermoderation
