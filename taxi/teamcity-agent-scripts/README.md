Buildagent package for Yandex Taxi TeamCity projects
==========================================================
## Run linters/formatters (need [taxi-deps-py3](https://a.yandex-team.ru/arc_vcs/taxi/deps-py3#installation))

#### Run in all repository / run only on changed files
* `make check-pep8`  / `make smart-check-pep8` - python linter
* `make format` / `make smart-format` - taxi formatter
* `make test` - tests

### Running Tier 0 tests locally

`ya make -A ./tests`

See more at https://docs.yandex-team.ru/devtools/test/manual
