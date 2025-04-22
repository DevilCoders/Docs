# Подготовка треков (привязка сигналов)

Регулярный процесс подготовки нужных для других процессов данных. Готовятся такие данные:
| Данные | Описание |
--- | ---
| signals | Сигналы от пользователей (схематизированные из логов [dispatcher'а](/arc/trunk/arcadia/maps/analyzer/services/jams_analyzer/modules/dispatcher)) |
| travel times | Треки, привязанные так же, как это происходит в онлайне в [usershandler'е](/arc/trunk/arcadia/maps/analyzer/services/jams_analyzer/modules/usershandler) |
| assessors | "Эталонные" треки, используемые при оценке качества, нарезанные по событиям роутера |

Данные за какой-то день, если они есть, то есть сразу все, и приматченные к одной версии графа.

### Нарезка асессоров

Асессоры режутся по:
- событиям роутера (запросы на маршруты, перестроения)
- по медленным проездам (заметно медленнее окружающих)

### Результаты

[Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/data)
[Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data)
