## Набор артефактов для сборки debian пакетов и docker образов.

Переведено на использования arcadia и ya package.

версии берутся из файлов pkg.json

### debian

для того что бы настроить хост для сборки пакетов надо:
<pre>
sudo apt-get install dh-systemd
sudo apt-get install devscripts
sudo apt-get install debhelper
</pre>

выполняем гайд: https://wiki.yandex-team.ru/infrasearch/common/debpackaging/ для генерации gpg ключей

после этого для сборки надо выполнить команду:
<pre>
ya package debian_pkg.json --debian
</pre>
в load/projects/yandex-tank-internal-pkg
Результат появится там же в виде tar.gz архива с деб пакетом и информацией о сборке

### docker

для сборки и заливки докер образа надо выполнить команду:
<pre>
ya package docker_pkg.json --docker --docker-repository load --docker-push
</pre>
в load/projects/yandex-tank-internal-pkg

описание есть тут: https://wiki.yandex-team.ru/yatool/package/?#vnimanie
на машине должен быть установлен docker и настроен login с доступом на заливку в load


## нюансы и ссылки
* Статья о том, как управлять плагинами jmeter из консоли: https://jmetervn.com/2016/12/14/how-to-install-plugins-in-jmeter-3-x-via-command-line/
