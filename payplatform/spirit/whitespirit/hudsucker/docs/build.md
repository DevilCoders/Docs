Пакеты, необходимые для сборки
 - `apt-get install ruby ruby-dev rubygems build-essential liblua5.3-dev devscripts`

Установить [fpm](https://fpm.readthedocs.io/en/latest/installing.html)
 - `gem install --no-ri --no-rdoc fpm`

Поправить шаблон для создания \*.changes файла, который находится примерно здесь `/var/lib/gems/2.5.0/gems/fpm-1.10.2/templates/deb/deb.changes.erb`:
 - добавить надо `Changed-By: <%= maintainer %>`

Запустить сборку
 - `./fpm_build.sh "1.0.6" 'Kirill Isupov (yandex-deb-sign) <isupov@yandex-team.ru>'`
