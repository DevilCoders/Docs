# Отчет метрики KGB в картах

KGB — (никак не расшифровывается) метрика, направленная на определение соотношения количества багов, найденных командой
сервиса, и багов, найденных всем остальным миром.
Графики представлены в:
| Сервис | Ссылки |
|:------------- |:-------------:|
| Реактор | https://reactor.yandex-team.ru/browse/resolve?path=/maps/analytics/reports/qa/kgb/web-maps/daily |
| Отчёт для БЯК | https://stat.yandex-team.ru/Maps/qa/kgb/ |


## Основная информация
Отчет собирает данные из Стартрека, выгруженные в YT.

Отфильтровываем тикеты по принципу:
* Баги, найденные за последние 30 дней в продакшне
* Резолюция или пустая, или отличается от "Не будет пофикшено", "Не воспроизводится", "Не валидный", "Дубликат"

Отсортировываем по двум критериям:
* По cеверити (миноры+тривиалы и нормалы+критикалы)
* По автору бага (команда сервиса и все остальные)

## Делаем в рамках задачи
https://st.yandex-team.ru/MAPSINFRA-2216
