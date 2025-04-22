# Iconostasinator
[![Screeenshot](https://jing.yandex-team.ru/files/alexunix/Iconostasinator.jpg)](https://jing.yandex-team.ru/files/alexunix/Iconostasinator.jpg)  
Handy app for auto-arranging monitoring panels using pre-build configs.

# Downloads
## [1.1.4](https://jing.yandex-team.ru/files/alexunix/Iconostasinator-15.zip)
- never bothered to finish refactor
- change panels sync url
## [1.1.3](https://jing.yandex-team.ru/files/alexunix/Iconostasinator-14.zip)
- Intermediate update before full refactor
  - Change icon
  - Change MartyDB source to warden
## [1.1.2](https://jing.yandex-team.ru/files/alexunix/Iconostasinator-13.zip)
- Right-click context menu for panels
  - Screenshots to jing or buffer
  - Make window draggable or borderless toggle
  - Copy panel URL
- Show window bounds when moving or resizing
- Open browser on navigating instead of new window
- Use removed windows bounds when replacing panels
- Dark Mode toggle (yasm only, others don't have dark mode?)
## [1.1.1](https://jing.yandex-team.ru/files/alexunix/Iconostasinator-12.zip)
- Notify about extra panels in config if doing manual sync with MartyDB
#### Old versions
[1.1.0](https://jing.yandex-team.ru/files/alexunix/Iconostasinator-11.zip)
[1.0.9](https://jing.yandex-team.ru/files/alexunix/Iconostasinator-10.zip)
[1.0.8](https://jing.yandex-team.ru/files/alexunix/Iconostasinator-9.zip)
[1.0.7](https://jing.yandex-team.ru/files/alexunix/Iconostasinator-8.zip)
[1.0.6](https://jing.yandex-team.ru/files/alexunix/Iconostasinator-7.zip)
[1.0.5](https://jing.yandex-team.ru/files/alexunix/Iconostasinator-5.zip)
[1.0.4](https://jing.yandex-team.ru/files/alexunix/Iconostasinator-4.zip)
[1.0.3](https://jing.yandex-team.ru/files/alexunix/Iconostasinator-3.zip)
[1.0.2](https://jing.yandex-team.ru/files/alexunix/Iconostasinator-1.zip)
[1.0.1](https://jing.yandex-team.ru/files/alexunix/Iconostasinator.zip)
[1.0.0](https://jing.yandex-team.ru/files/alexunix/Iconostasinator.app.zip)

# Usage

Default configuration asssumes 4 screens in 4k resolution and in portrait mode.
Arrange screens similar to provided screenshot below and launch app.

[![4mon-setup](https://jing.yandex-team.ru/files/alexunix/4mon-setup.png)](https://jing.yandex-team.ru/files/alexunix/4mon-setup.png)

## Development (OSX)

Get homebrew and node.

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
brew install node
```

Install dependencies.

```sh
npm i
```

Get arc token and place to oauth.json.

Start in development mode.

```sh
npm start
```

Also check out docs and Electron Fiddle:  
https://www.electronjs.org/docs  
https://www.electronjs.org/#get-started


## Building (OSX)

Build binary for OSX.

```sh
npm run build-osx
```
Binary will be in `./build` dir.
