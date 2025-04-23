# Mobile web application

Sovetnik mobile web application.

## Requirements

-   [nvm](https://github.com/creationix/nvm)
-   node (see version in [.nvmrc](.nvmrc))

## Setup

### Clone the repo

This command will download `mobile-app` repo to your local environment:

```sh
git clone git@github.yandex-team.ru:sovetnik/mobile-app.git
```

### Install dependencies

```sh
cd mobile-app
```

If you have the right version of [node](.nvmrc):

```sh
nvm use && npm i
```

If not:

```sh
nvm install <node_version_from_nvmrc_file>
npm i
```

## Build

### Development

#### Using script injection

```sh
# Yandex Browser
npm run dev

# Smart Search browser
npm run dev:smart_search

```

#### Using browser extension

1. Run this command:
```sh
# Yandex Browser
npm run dev:ext
```

2. Load `extension` folder as an extension to your browser

3. Click on extension icon on any product page

You can use *watch mode* too:

```sh
npm run dev:ext:watch
```


### Production

```sh
# build all production-ready extensions
npm run build

# build UC Web
npm run build:uc

# build Yabro
npm run build:yabro

# build Yabro (Huawei)
npm run build:yabro:huawei

# build Smart Search browser (iPhone and Android)
npm run build:smart_search

# build Smart Search browser (iPhone only)
build:smart_search:iphone

# build Smart Search browser (Android only)
build:smart_search:android
```

## Storybook

You can view all our components using this command:

```sh
npm run storybook
```
