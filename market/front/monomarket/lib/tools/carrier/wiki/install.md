# Установка ya tool

1. выполняем [Системные требования](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#system-requirements) и [Установку Arc](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#arc-setup) из инструкции: [Быстрый старт](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)

2. Монтируем arc
Для удобного монтирования/размонтирования арка я использую пару скриптов которые положил в локальную папку которую предварительно прописал в PATH:

*arc-mount*
```bash
#!/usr/bin/env bash
set -e

mkdir -p /home/gheljenor/arc/arcadia /home/gheljenor/arc/store

pushd /home/gheljenor/arc
nice arc mount -m arcadia/ -S store/
popd
```

*arc-umount*
```bash
#!/usr/bin/env bash
set -e

arc unmount /home/gheljenor/arc/arcadia
```

3. Добавляем arc/arcadia в PATH. Для этого нужно прописать строчку вида `PATH=$PATH:/home/gheljenor/arc/arcadia` к себе в `~/.bashrc` или аналогичный конфиг (зависит от окружения).

4. proffit!

# Установка carrier

```bash
npm i -g @yandex-market/carrier
```

# Проверка

Проверить, что всё установленно успешно можно вызвав `carrier` в самом репозитории carrier. В случае правильной настройки будут успешно установлены node_modules.