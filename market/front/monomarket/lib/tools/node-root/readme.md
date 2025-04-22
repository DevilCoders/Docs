# Node root

Замена для `git rev-parse --show-toplevel` / `arc rev-parse --show-toplevel`, которая работает на любых файловых системах и системах котроля версий.

## Установка

```shell
npm install -g @yandex-market/node-root
```

## Использование

```shell
node-root [pkg-name] # если не указывать название пакета, будет найдет первый попавшийся корень с package.json
```

Также можно использовать эту команду через npx. Однако стоит помнить про баг с кешом в нашей инсталляции npm.

```shell
~/work/monomarket/lib/lib/yammy-lib > npx --cache $(mktemp -d) @yandex-market/node-root 2>/dev/null
/home/gheljenor/arc/arcadia/market/front/monomarket/lib/lib/yammy-lib
~/work/monomarket/lib/lib/yammy-lib > npx --cache $(mktemp -d) @yandex-market/node-root @yandex-market/monomarket 2>/dev/null
/home/gheljenor/arc/arcadia/market/front/monomarket
```
