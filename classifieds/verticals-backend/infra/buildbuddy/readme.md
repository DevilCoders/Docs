#buildbuddy.io

Для сборки новой версии:
```bash
make build BUILDBUDDY_VERSION=v2.5.2 # заменить версию на свою
```

Если нужно выпустить патч:
```bash
make build BUILDBUDDY_VERSION=v2.5.2 VERSION=v2.5.2-vertis1 #базовая версия и наша версия
```