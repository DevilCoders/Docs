# infra-cfg-juggler
Config templates for Juggler monitoring (https://wiki.yandex-team.ru/SM/Juggler/).
Configs are generated and pushed to Juggler every 30 minutes from [%taxi_infra_tools](https://c.yandex-team.ru/groups/taxi_infra_tools)

## scripts
#### add_template.py
This script is useful when you need to add a template to multiple check-files.
The following example adds template 'hejmdal-rtc-resource-usage' to all stable rtc checks:
`$ infra-cfg-juggler: python3 scripts/add_template.py --dir 'checks' --template 'hejmdal-rtc-resource-usage' --mask 'rtc_.*_stable'`

#### api-proxy/generate.py
This scripts generates solomon alerts and juggler checks settings for api-proxy handlers. Each handler's alerts and checks are stored in a separate file, where there is a service for each of the handler's resources. It is possible to configure thresholds per resource and/or change the list of resources via `settings.yaml` config file.

Note: this scripts requires `jinja2` and `pyyaml` packages

## Run tests

`make test`

## Automerge 
Для того, чтобы вмержить мониторинги своего сервиса, без привлечения и отвлечения эксплуатации, должны выполниться следующие требования:
* ПР прошёл тесты
* ПР окнут (нет ни одного request changes запроса)
* добавлена метка (lable) automerge
* автор и/или ревьюеры являются ответственными (1) за **все** затронутые сервисы (2) (3)

(1) ответственный за сервис - все дежурные и мейнтейнеры сервиса. Учитываются только те сервисы, для которых разработка забрала на себя круглосуточный мониторинг, иначе - ответственных нет === эксплуатация

(2) проверяются все затронутые в ПРе check файлы, по ним определяются и находятся сервисы в клоуне. Если сервис не получилось определить или он не известен для клоуна - автомержа не произойдёт

(3) все мониторинги, сделанные через соломон приравниваются к полностью разработческим и не участвуют в определении затронутых сервисов и определении ответственных

### Особые случаи
Если ПР затрагивает **только** соломоновские проверки - проверки на ответственных не происходит - достаточно только первых 3х условий

При построении списка ответственных, берётся пересечение **всех** ответственных за **все** затронутые сервисы. Таким образом, если ПР затрагивает сервисы A и B, но автор является ответственным только за A, а аппрувер - только за B -- мерж невозможен. Нужно либо найти человека с достаточным уровнем ответственности, либо попросить проверить и вмержить эксплуатацию.

При редактировании *тестов*, *шаблонов* и/или *telegram_options* - необходимо попросить посмотреть эксплуатацию.
