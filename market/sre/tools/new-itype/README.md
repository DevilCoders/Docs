# new-itype
> A tool for creating an itype at https://gencfg.yandex-team.ru and a config for the YASM agent

## Usage example

It can be build and used locally. In case you do not have arcadia follow the instruction [here](https://wiki.yandex-team.ru/yatool/distrib/).
```
> ya make --checkout market/sre/tools/new-itype 
> new-itype/new-itype --help
Usage: new-itype [OPTIONS] ITYPE

  This tool creates a new itype at https://gencfg.yandex-team.ru and adds
  YASM config to https://bb.yandex-
  team.ru/projects/SEARCH_INFRA/repos/yasm/browse.

Options:
  --debug
  --dry-run           Do not change anything.
  --ssh-key PATH      Private ssh key file.
  --ticket TEXT       Startrek ticket key, e.g. CSADMIN-1111.  [required]
  --description TEXT  Service description.
  --help              Show this message and exit.
  --version           Show the version and exit.
>
> market/sre/tools/new-itype/new-itype myitype --description 'My itype' --ticket TEST-1111
```

Though the easiest way is to build and run at [Sandbox](https://sandbox.yandex-team.ru/), e.g. https://sandbox.yandex-team.ru/task/210838867/view.

## Links

http://wiki.yandex-team.ru/market/administration/new-rtc-service/
https://tsum.yandex-team.ru/pipe/projects/sre/release/new/rtc-new-service
