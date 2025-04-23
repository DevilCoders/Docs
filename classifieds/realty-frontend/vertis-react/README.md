Storybook
---
https://s3.mds.yandex.net/vertis-frontend-private/realty-storybook/index.html

Локальная разработка
---

Сторибук можно поднять локально:
```sh
make deps
make storybook
```

Публикация новой версии выполняется автоматически через Github Action при мерже в мастер.

Troubleshooting
---
Проблема: на macOS ошибка при установке зависимостей `⚠ mozjpeg pre-build test failed`

Решение:
```sh
brew update
brew install automake autoconf libtool dpkg pkgconfig nasm libpng
rm -rf node_modules
make deps
```
