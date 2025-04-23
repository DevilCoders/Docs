# Jupyter Kernel DWH

## Как собрать пакеты

Пока у нас нет агента для сборки пакетов под Bionic, они собираются руками.

Сделать это можно на виртуалке, которую поднимает jupyter.yandex-team.ru.

Процедура такая:


Копируем GnuPG ключ на виртуалку, или создаём его там. Email и в debian/changelog
и в ключе должен быть корповый. Как создать ключ:
https://wiki.yandex-team.ru/taxi/backend/taximeter/sborka-kastomnyx-paketov/#prerequisites

Далее, ставим зависимости, нужные для сборки:

```bash
sudo apt-get install devscripts equivs debhelper dh-virtualenv yandex-dh-environment unixodbc dupload
```

Собираем `dmp-deps`:

```bash
cd ~/dwh/dmp_deps

# тут надо отредактировать debian/changelog и заменить у последней записи
# buildfarm <buildfarm@yandex-team.ru> на своё имя и email:

vim debian/changelog
debuild --no-lintian --check-dirname-level 0 --no-tgz-check -b
```

Собираем пакет с DWH Kernel:

```bash
cd ~/dwh/
git submodule init
git submodule update

cd ~/dwh/jupyter

dch -i

# Заполняем changelog данными полученными путём просмотра:
# git log -- ../dmp_suite/dmp_suite/jupyter

debuild --no-lintian --check-dirname-level 0 --no-tgz-check -b
```

Загружаем пакетики в репозиторий:

Если конфига ~/.dupload.conf нет, то его надо предварительно создать:

```bash
cat > ~/.dupload.conf <<EOF
package config;

$cfg{'yandex-taxi-bionic'} = {
    fqdn => "yandex-taxi-bionic.dupload.dist.yandex.ru",
    method => "scpb",
    incoming => "/repo/yandex-taxi-common/mini-dinstall/incoming",
    dinstall_runs => 0,
};
EOF
```

Потом зовём `dupload`:

```bash
cd ~/dwh/
dupload --to yandex-taxi-bionic --nomail
```

При старте ядро автоматически проверяет, есть ли обновления и предлагает пользователю вызвать команду `%update`.

## Как использовать ядро в dev окружении

* `pip install jupyter commonmark`
* `jupyter kernelspec install jupyter/kernel-dev --name 'taxi-dwh-dev' --user`
* `jupyter notebook --no-browser --ip $(hostname -f)`

В запустившемся Jupyter нужно выбрать ядро "Taxi DWH (dev)".

Подробнее про устройство Jupyter ядра [читай на вики](https://wiki.yandex-team.ru/taxi/dwh/dmpasplatform/dmpdev/jupyter-dev/).
