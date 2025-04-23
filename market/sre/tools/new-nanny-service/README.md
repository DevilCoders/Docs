# new-nanny-service
> A tool for creating Nanny services from a template

## Usage example

It can be build and used locally. In case you do not have arcadia follow the instruction [here](https://wiki.yandex-team.ru/yatool/distrib/).
```
> ya make --checkout market/sre/tools/new-nanny-service
> market/sre/tools/new-nanny-service/new-nanny-service --help
Usage: new-nanny-service [OPTIONS] SERVICE:GROUP...

  This tool creates Nanny services from a template service. The argument
  SERVICE:GROUP can be passed multiple times.

Options:
  --debug
  --allow-override               Allow override existing services or do not.
  --ssh-key PATH                 Private ssh key file.
  --description TEXT             Service description.
  --template-service-id TEXT     Template Nanny service id.
  --gencfg-release TEXT          Gencfg release.
  --sandbox-resource-id INTEGER  Sandbox resource id of application's tarball.
                                 [required]
  -g, --owners-group INTEGER     Staff group id.
  -l, --owners-login TEXT        Staff login.
  --help                         Show this message and exit.
  --version                      Show the version and exit.
>
> market/sre/tools/new-nanny-service/new-nanny-service testing_market_my_service_sas:SAS_MARKET_TEST_MY_SERVICE --sandbox-resource-id 0
```

Though the easiest way is to build and run at [Sandbox](https://sandbox.yandex-team.ru/), e.g. https://sandbox.yandex-team.ru/task/206970350/view.

**Пример** запуска для копирования сервиса production_market_new_sevice_sas в testing_market_esokolov_test_sas на основе YP-Lite с квотой в ABC:37574
одним инстансом, 1000 мс CPU, 1024 Mb RAM, сетевым макросом _GENCFG_MARKET_TEST_, носителем типа hdd, и с квотами на корень и рабочую директорию в 1Гб и 1Гб.
```
/new-nanny-service -l e-a-sokolov --app-sandbox-resource-id 0 --abc-service-id 37574 --service-category '/market' --template-service-id production_market_new_sevice_sas testing_market_esokolov_test_sas:YP:37574:esokolov:1:1000:1024:_GENCFG_MARKET_TEST_:hdd:1:1
```

## Links

http://wiki.yandex-team.ru/market/administration/new-rtc-service/
https://tsum.yandex-team.ru/pipe/projects/sre/release/new/rtc-new-service
