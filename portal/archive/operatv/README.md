# opera-tv-www
Морда для телевизоров hw.yandex.ru/op

Для разработки не нужен бэкенд, достаточно сконфигурировать эту морду конфигуратором, который сгенерирует конфиг nginx:

Допустим ваш dev - v111.wdevx.yandex.ru

Instance - v111d1
(основную морду из инстанса не удалять)

Ваш login - MyLogin
```
ssh v111.wdevx.yandex.ru
cd /opt/www
sudo git clone https://github.yandex-team.ru/morda/operatv.git opera-v111d1
cd opera-v111d1/
sudo chown MyLogin . -R
vi configurator/configurator.conf
```
Конфигурационный файл откроется в редакторе VIM. Файл необходимо отредактировать следующим образом.
(Отредактированный файл сохранить, но не коммитить)
```
<Configfile nginx-opera>
    Mode        tune
    Filename    {SUBNAME}/nginx-opera.ngx
    Template    nginx-opera.conf.template
    Deploy      /etc/nginx/sites-enabled/opera-{SUBNAME}.ngx
</Configfile>

<Devproxy>
    Subdomain   wdevx
</Devproxy>

<Devmachine v111>
    Uname   v111.vla.yp-c.yandex.net
    Address v111.vla.yp-c.yandex.net

    Wildcard v111*
</Devmachine>

<Instance v111d1>
    Datacenter  second
    Devinstance yes
</Instance>

<DefaultInstance>
    Base        /opt/www/opera
    ConcatDevinstanceBase yes
</DefaultInstance>      
```
Сохраняем файл и продолжаем
```
git submodule update --init
make
sudo ./configurator/configurator.pl -d v111d1
sudo ./configurator/configurator.pl -d v111d1
sudo service nginx restart
```
Морда станет доступна по адресу 
```
opera-v111d1.wdevx.yandex.ru
```

Для того, чтобы увидеть сделанные изменения, морду необходимо пересобрать
```
make clean all
make
```

## Приложение для телевизоров samsung
Тоже собирается из этого же кода через `make archive PACKAGE=(tizen|orsay)`

Явки-пароли в этом таске https://st.yandex-team.ru/HOME-37319

## Пакеты
`opera-tv-www` `opera-tv-www-static` в репозитории `verstka`
