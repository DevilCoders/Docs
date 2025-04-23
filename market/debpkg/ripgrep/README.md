Скачать musl-сборку отсюда:

https://github.com/BurntSushi/ripgrep/releases

извлечь только бинарь rg и положить в usr/bin/

dch -i

dpkg-buildpackage -b -rfakeroot -us -uc

debsign <ripgrep-blablabla>.changes

dupload --to=common <ripgrep-blablabla>.changes

