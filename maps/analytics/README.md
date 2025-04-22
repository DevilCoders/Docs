# Аналитика Карт

## Основная информация
| Сервис | Путь |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-analytics |
| Arcadia | [/arcadia/maps/analytics](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics) |
| Cofe | [/arcadia/quality/ab_testing/cofe/projects/maps](https://a.yandex-team.ru/arc/trunk/arcadia/quality/ab_testing/cofe/projects/maps) |
| YT | [hahn.home/maps/analytics](https://yt.yandex-team.ru/hahn/navigation?navmode=acl&path=//home/maps/analytics) (аккаунт [maps-analytics](https://yt.yandex-team.ru/hahn/accounts/general?filter=maps-analytics)) |
| YT (pool) | [maps-analytics](https://yt.yandex-team.ru/hahn/scheduling/overview?pool=maps-analytics&tree=physical) для обычных регулярных расчетов; [maps-analytics-privileged](https://yt.yandex-team.ru/hahn/scheduling/overview?pool=maps-analytics-privileged&tree=physical) для регулярных расчетов с SLA; [maps-research](https://yt.yandex-team.ru/hahn/scheduling/overview?pool=maps-research&tree=physical) для adhoc расчетов |
| Nirvana | [Maps.Analytics](https://nirvana.yandex-team.ru/quota/geo-analytics)  |
| Reactor | [/maps/analytics](https://nirvana.yandex-team.ru/browse?selected=2990531) |
| Sandbox | [MAPS_ANALYTICS](https://sandbox.yandex-team.ru/admin/groups/MAPS_ANALYTICS) |
| Vault | https://yav.yandex-team.ru/ (тег `maps-analytics`) |
| Robot | https://staff.yandex-team.ru/robot-maps-analytics |
| Robot CI | https://staff.yandex-team.ru/robot-maps-analyt-ci |
| DataLens | [/maps/analytics](https://datalens.yandex-team.ru/navigation/b66f2x1qdhke7-analytics)|
| Чат инфраструктуры | [Slack](https://join.slack.com/share/zt-jfgq9obr-8WV8gxokWri3A1wa9TrBjg?cdn_fallback=1), [Telegram (для тех, кто не в Slack)](https://t.me/joinchat/BEZLVw5QJeN_7DMxzSn5FQ) |
| Фичреквесты | https://wiki.yandex-team.ru/maps/analytics/buddata/plan/wishes/ |

## Структура
### Arcadia/YT/Reactor
| Директория | Описание |
|---|---|
| `logs` | Выжимки логов карт и навигатора в поколочном и предобработанном формате|
| `datasets` | Датасеты – подготовленные данные для быстрого решения частых задач |
| `metrics` | Конфиги фичей и метрик над датасетами |
| `data` | Данные не подходящик к logs |
| `reports` | Расчет с публикацией данных в отчеты Яндекс.Статистики |
| `reports/datasets` | Стандартные отчеты метрик (`metrics`) над датасетом (`datasets`) |
| `st` | Результаты работ над задачами из Трекера. Формат хранения `st/<название очереди>/<номер тикета>-<короткое описание>`  |
| `legacy` | Расчет (джобы и экшены) [перенесенные из JAM (RJM)](https://st.yandex-team.ru/MAPSINFRA-2494) |

### Arcadia
| Директория | Описание |
|---|---|
| `docs` | Документация и инструкции |
| `lib` | Библиотека функций для `python` и `YQL` |
| `tools` | Инструменты для разработки и администрирование инфраструктуры аналитики |
| `tests` | Тесты |
| `CONTRIBUTING.md` | Инструкция про настройку окружения |

### YT
- Все регулярные расчеты хранятся в тех же папках на YT, что и код в Аркадии
- Разовые расчеты храним согласно таблице ниже:

| Директория | Описание | Примеры |
|---|---|---|
| `home/maps/analytics/st/<название очереди>/<номер тикета>-<короткое описание>` | Результаты работ над задачами из Трекера. Хранится примерно 1.5 года. Не поленитесь создать/указать тикет, если хотите хранить данные в квоте Карт | `//home/maps/analytics/st/GEOANALYTICS/1429-zapravki-in-tabbar/`
| `home/maps/analytics/tmp/<login>` | Для временных результатов. Автоматическое удаление через 30 дней после создания. |  Тестовые расчеты; данные без привязки к тикету  |

## Гостевой доступ
Чтобы получить доступ на чтение, попросите вас добавить в ABC-сервис [maps-analytics-users](https://abc.yandex-team.ru/services/maps-analytics-users/).

## Мониторинги
| Сервис | Путь |
|---|---|
| Telegram | [MapsAnalyticsMonitorings](https://t.me/joinchat/BEZLVxQahxMbhT99ls1wSg) |
| Solomon | [maps-analytics](https://solomon.yandex-team.ru/admin/projects/maps-analytics/) |
| Juggler checks | [geo.maps-analytics](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-analytics%26namespace%3Dgeo.maps-analytics) |


## Workflow
Шаблонные воркфлоу находятся [тут](https://reactor.yandex-team.ru/browse?selected=10172208)

Карантинные воркфлоу находятся [тут](https://reactor.yandex-team.ru/browse?selected=10172209)

Все кастомные воркфлоу, которые нельзя свести к шаблонным храним рядом с расчетом с названием `/path/daily_workflow`

Правила дорабоки шаблонных воркфлоу:
- Клонируем сохраненный `Main` граф и дорабатываем/правим граф => получаем новую версию графа
- Переводим свой расчет на новую версию (нужно заменить в конфиге `lama.yaml` `workflow_id` на `instance_id` и тогда будет использоваться конкрентый граф)
- Переводим еще несколько расчетов на новую версию
- Если все ок, новому воркфлоу задаем `Set Main`
- Все новые инстансы берутся из `Main`

### Кубик YQL
- Передаем параметры как массив
- Передаем target без слеша вначале
- Передаем в target полностью путь до кода YQL


## CI and lama-sync

- При вливании коммита в `trunk` создаются артефакты [lama-actions](https://reactor.yandex-team.ru/browse/resolve?path=%2Fmaps%2Fanalytics%2Ftools%2Flama-actions) для всех измененных файлов `lama.yaml`, по которому запустится реакция [lama-sync](https://reactor.yandex-team.ru/browse/resolve?path=%2Fmaps%2Fanalytics%2Ftools%2Flama-sync)

- Fallback в 6 часов утра для всей папки [maps-analytics](https://reactor.yandex-team.ru/browse/resolve?path=%2Fmaps%2Fanalytics)
- Можно вручную запустить реакцию `lama-sync` или инстанциировать артефакт `lama-actions` c нужным значением конфига
