# YDL UI
UI for [(yet another) timeline service](https://github.yandex-team.ru/YAPPY/YDL).

### Documentation

[Wiki](https://wiki.yandex-team.ru/jandekspoisk/sepe/YaDeLorean)

### Installation
Checkout source code:

```bash
git clone git@github.yandex-team.ru:YAPPY/YDL-UI.git
```

Fetch submodules:

```bash
cd ydl-ui
git submodule init
git submodule update
```

Install dependencies:

```bash
npm install
```

### Building
Development build:

```bash
npm run build             # development
npm run build_production  # production
```

### Using UI bundle with YDL sources
Copy built bundles to `ydl/src/timeline/static/timeline` directory:

```bash
cp /path/to/ydl-ui/dist/*.{css,js,map} /path/to/ydl/src/timeline/static/timeline
```
