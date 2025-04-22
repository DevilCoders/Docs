# new-nanny-dashboard
> A tool for creating Nanny dashboard

## Usage example

It can be build and used locally. In case you do not have arcadia follow the instruction [here](https://wiki.yandex-team.ru/yatool/distrib/).
```
> ya make --checkout market/sre/tools/new-nanny-dashboard
> market/sre/tools/new-nanny-dashboard/new-nanny-dashboard --help
Usage: new-nanny-service [OPTIONS] SERVICE:GROUP...

  This tool creates Nanny dashboard for existing nanny services

Options:
  --debug
  --dashboard-id                 dashboard id, required
  -g, --owners-group INTEGER     Staff group id.
  -l, --owners-login TEXT        Staff login.
  --help                         Show this message and exit.
  --version                      Show the version and exit.
>
> market/sre/tools/new-nanny-dashboard/new-nanny-dashboard dash_id login group testing_market_my_service_sas:SAS_MARKET_TEST_MY_SERVICE
```

Though the easiest way is to build and run at [Sandbox](https://sandbox.yandex-team.ru/)

