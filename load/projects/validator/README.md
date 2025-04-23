# yandex-tank-validator

internal validator.
to run localy you need to set environmenr:
```bash
export APPLICATION_SETTINGS=~/app_settings.ini
cp docker/app_settings.ini ~/app_settings.ini
>application.log
```
build validator with ya make, and run it through:
```bash
./bin/vaildator -p <port> -w <uwsgi_worker_num>
```

### Cборка docker образа

для сборки и заливки докер образа надо выполнить команду:
<pre>
ya package pkg.json --custom-version=<versiontag> --docker --docker-repository <folder> --docker-push
</pre>
в load/projects/validator

описание есть тут: https://wiki.yandex-team.ru/yatool/package/?from=%252Fyatool%252Fsandbox%252Fyapackage%252F#vnimanie
на машине должен быть установлен docker и настроен login с доступом на заливку в заливаемую папку
