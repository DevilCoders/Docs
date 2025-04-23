ITS client
----------

Client for [Instance Tune System](https://beta.wiki.yandex-team.ru/jandekspoisk/sepe/nanny/its/).

Installation:

```
virtualenv its_client_env
. its_client_env/bin/activate
pip install -U its_client -i http://pypi.yandex-team.ru/simple/
```

Usage:

```
its_client -c its_client_config.yml
```

Config example is available in `cfg_default.yml` file in this repository.

Wiki: https://beta.wiki.yandex-team.ru/JandeksPoisk/Sepe/itsclient/
