# Advertising Admin [![Build Status](https://drone.yandex-team.ru/api/badges/advertising/adv-admin/status.svg)](http://drone.yandex-team.ru/advertising/adv-admin)

## Как запустить локально

В первую очередь скачиваем и устанавливаем [brew](https://docs.brew.sh/Installation) – универсальный пакетный мендежер для MacOS, Linux и Windows 10. И Docker для [MacOS](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) или [Linux](https://docs.docker.com/install/linux/docker-ce/ubuntu/).

```sh
# Устанавливаем NVM (не забываем выполнить инструкции от Brew в секции Caveats)
brew install nvm

# Устанавливаем Node.js 10 версии
nvm install 10

# Устанавливаем зависимости
npm run deps

# Устанавливаем Canvas
npm run deps:canvas

# Запускаем сборку и magicdev – локальный сервер
npm run dev
```
