# TZDATA

Из-за переезда Волгограда и области в зону RTZ-2 были в экстренном порядке собраны пакетики с версиями tzdata_2020e-0yandex~ubuntu{12,14,16,18,20}.04 и залиты в соответствующие репозитории yandex-<oscodename>/unstable.

## Сборка пакетов
Подготавливаем сборочное окружение:

    sudo tee /etc/apt/sources.list.d/mirror-src.list <<EOF
    deb-src http://mirror.yandex.ru/ubuntu $(lsb_release -cs) main restricted universe multiverse
    deb-src http://mirror.yandex.ru/ubuntu $(lsb_release -cs)-security main restricted universe multiverse
    deb-src http://mirror.yandex.ru/ubuntu $(lsb_release -cs)-updates main restricted universe multiverse
    EOF

    sudo apt-get udpate
    sudo apt-get -y install build-essential devscripts debhelper dupload lzip

Копипастим секретный gpg-ключ (`gpg --export-secret-keys --armor`) и скармливаем его в `gpg --import`

Создаем директорию для сборки:

    mkdir build
    cd build
    apt-get source tzdata
    curl -O https://data.iana.org/time-zones/releases/tzdb-2020e.tar.lz
    lzip -d tzdb-2020e.tar.lz
    gzip tzdb-2020e.tar
    mv tzdb-2020e.tar.gz tzdata-2020e.orig.tar.gz
    mkdir tzdata
    cd tzdata
    tar zxvf ../tzdata-2020e.orig.tar.gz
    tar Jxvf ../*debian*


Отдельный шаг для древних дистрибутивов (precise, trusty): выковыриваем из orig версии дистрибутива файлики systemv и newpacific, кладем их в build/tzdata (туда же, куда распаковали остальное) и добавляем в tzdata-2020e.orig.tar.gz (иначе придется оформлять патч для пакета).

Добавляем запись в debian/changelog (показываю пример) с новой upstream-версией и билдом с минимальным приоритетом:

    tzdata (2020e-0~yandex~ubuntu12.04) xenial; urgency=medium

      * New upstream version

     -- Anton Suvorov <warwish@yandex-team.ru>  Wed, 23 Dec 2020 03:43:23 +0300

Пробуем собрать пакетик командой `debuild`. Если все хорошо - вводим пароль для подписи когда попросят или смотрим в ошибку и пытаемся ее исправить (скорее всего не будет хватать пакетиков, которые просто нужно будет доустановить с помощью `sudo apt-get install`). После исправления ошибок собираем и подписываем пакет командой `debuild`.

Заливаем собранный пакет в нужный репозиторий:

    # example dupload conf
    warwish@warwish-build-xenial:~$ cat ~/.dupload.conf
    package config;

    $cfg{'yandex-xenial'} = {
        fqdn => "duploader.yandex.ru",
        method => "scpb",
        incoming => "/repo/yandex-xenial/mini-dinstall/incoming/",
        dinstall_runs => 0,
    };

    cd build
    dupload --to <repo> --nomail <filename>.changes
