# Фронтэнд карт

Страничка проекта на вики: [maps](https://wiki.yandex-team.ru/maps/dev/ui/products/maps/).

-   [Workflow](docs/workflow.md)
-   [Конфигурация проекта](docs/config.md)
-   [SEO](docs/seo.md)
-   [Рассылки](docs/mail.md)

Технологии:

-   [React](docs/react.md)
-   [Typescript](docs/typescript.md)

## Требования к системе

-   Ключи ssh/gpg с локальной машины на [staff](https://staff.yandex-team.ru/)
-   [nvm](https://github.com/creationix/nvm)
-   [arc](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)

## Разработка

### Установка

```sh
cd /maps/front/services/maps
nvm use
# Настройка машины для локальной разработки.
make local-setup
```

### Запуск

```sh
make dev
# или
make love
```

Открыть `https://<username>.maps.dev.yandex.ru:8080/maps` в браузере.

#### Разные страницы

Также можно указать только нужные страницы, чтобы собиралось не всё сразу. Для этого определите переменную окружения `ENTRIES` (по умолчанию собираются все страницы):

```sh
ENTRIES=desktop,print make dev
```

Возможные значения смотри в [`webpack.config.js`](./webpack.config.js#L10-L20).

## Troubleshooting

##### xcode-select

Если возникла следующая проблема:

```sh
xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance
```

то необходимо прописать в командной строке:

```sh
sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
```

##### nvm

Если вы используете macOS, у вас может отсутствовать файл .profile
Для устранения этой проблемы вы можете запустить `touch ~/.profile` в командной строке и повторно запустить скрипт установщика.
Если после этого проблема не устранена, вы можете открыть существующий файл `vim ~/.profile` и добавить в него следующие строки:

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```

##### Ubuntu 18.04 и сборка пакетов

При выполнении `npm i` могут не собираться некоторые пакеты.

**@yandex-int/geobase6@1.3.1**

```
../src/geobase6/geobaselookup.h:3:10: fatal error: geobase6.hpp: No such file or directory
 #include <geobase6.hpp>
          ^~~~~~~~~~~~~~
compilation terminated.
```

Нужен пакет `libgeobase6-dev`.

```
apt-get install libgeobase6-dev
```

Но он не ставится, т.к. для 18.04 зависимости не удовлетворены: нужен `libprotobuf9v5`. Ставим его руками, скачать можно отсюда https://packages.ubuntu.com/xenial/libprotobuf9v5. Теперь `apt-get install` должен сработать.

**@yandex-int/langdetect@1.0.1**

```
> @yandex-int/langdetect@1.0.1 install .../@yandex-int/langdetect
...
../src/langdetect/detector.h:3:10: fatal error: langdetect/lookup.hpp: No such file or directory
```

Нужны пакеты `libyandex-lang-detect`, `libyandex-lang-detect-dev`, `yandex-lang-detect-data`.

```
apt-get install libyandex-lang-detect libyandex-lang-detect-dev yandex-lang-detect-data
```

Пакеты при установке (`apt-get install`) могут не находиться. В `/etc/apt/sources.list` надо добавить

```
deb http://dist.yandex.ru/yandex stable/all/
deb http://dist.yandex.ru/yandex-xenial stable/all/
deb http://dist.yandex.ru/yandex-xenial stable/amd64/
deb http://dist.yandex.ru/common stable/all/
deb http://dist.yandex.ru/common stable/amd64/
```

и после выполнить `apt-get update`.
