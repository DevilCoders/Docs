# Local Jupiter

## Config
jupiter_config.json should contain a dict of LocalJupiter arguments (kwargs).
You can find a list of all arguments in [robot/jupiter/library/python/local_jupiter/__init__.py](https://a.yandex-team.ru/arc/trunk/arcadia/robot/jupiter/library/python/local_jupiter/__init__.py) (`LocalJupiter.__init__`).
See example of jupiter_config.json in [junk/paxakor/local_jupiter_config.json](https://a.yandex-team.ru/arc/trunk/arcadia/junk/paxakor/local_jupiter_config.json)

## Launch using run.py
`./run.py --config /PATH/TO/CONFIG.json [--no-binaries] [--dist] [--no-checkout] [ya make arguments]`

## Manual launch
`ya make -rA --test-stderr --test-disable-timeout --test-param jupiter_config=/PATH/TO/CONFIG.json`
Add flag `-DNO_BINARIES` to avoid fetching and compiling large C++ binaries.

## Notes
* Do not forget to export your YT_TOKEN and YT_POOL!
