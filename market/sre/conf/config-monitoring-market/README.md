Сборка пакета debian:
ya package --debian -Zgzip pkg.json

Сборка пакета RHEL:
ya package --rpm rpmpkg.json

В результате будет собран tar архив с пакетами внутри. Распаковать его можно так:
tar -xvf config-monitoring-market.<version>.tar.gz

