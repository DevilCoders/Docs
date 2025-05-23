# Тиры надежности
 
Для классификации сервисов используется распределение по "тирам" надежности.  
Мы выделяем четыре тира: **A**, **B**, **C**, и **D**, где A это высший тир надежности.  
Распределение сервисов по тирам пересматривается по итогам каждого периода ревью.

Тиры надежности присваиваются для [вертикалей и горизонталей](verticals_horizontals) согласно таблицам для всех нижеперечисленных категорий:
- [Доступность](#tier-category-available)
- [Мониторинг](#tier-category-monitoring)
- [Документация](#tier-category-docs)
- [Дежурства](#tier-category-duty)
- [Релизы](#tier-category-releases)
- [Работа с инцидентами](#tier-category-incidents)
- [Регламентные работы](#tier-category-duty)

## Доступность {#tier-category-available}

Критерий | Примечание | Тир А | Тир В | Тир С | Тир D
:---: | :---: | :---: | :---: | :---: | :---:
Коэффициент доступности | Вертикаль | 99.99 | 99.95| 99.5 | -
Суммарный YDT за ревью период < N* | Вертикаль/Горизонталь | 250 | 500 | 1000 | -
Выполняется [SLA](service_levels) горизонтали | Горизонталь ||||

## Мониторинг {#tier-category-monitoring}
Критерий | Примечание | Тир А | Тир В | Тир С | Тир D
:---: | :---: | :---: | :---: | :---: | :---:
Есть [Disaster](disasters) алерты | Вертикаль/Горизонталь | + | + | + | +
Есть алерты для автоматического расчета [YDT](ydt) в инцидентах, а также их фоновых значений вне временных отрезков инцидентов | Вертикаль/Горизонталь | + | + | + | Приветствуется
Задан вес вертикали и всех ее функциональностей для расчёта метрики [YDT и YDTb](ydt) | Вертикаль | + | + | + | Приветствуется
У сервиса есть диагностическая панель | Вертикаль/Горизонталь | + | + |  |
Диагностическая панель передана в дежурную смену | Вертикаль/Горизонталь | + | | |
Алерты горизонтали переданы сервисам-потребителям | Горизонталь | + | + | + | Приветствуется
Получены алерты сервисов-провайдеров (горизонталей, которыми пользуется вертикаль) | Верткаль | + | + | + | Приветствуется 

## Документация {#tier-category-docs}
Критерий | Примечание | Тир А | Тир В | Тир С | Тир D
:---: | :---: | :---: | :---: | :---: | :---:
Инструкция для диагностики и починки типовых проблем в [Вардене](../../../tools/warden) | Вертикаль/Горизонталь | + | | |

## Дежурства {#tier-category-duty}
Критерий | Примечание | Тир А | Тир В | Тир С | Тир D
:---: | :---: | :---: | :---: | :---: | :---:
Организованы дежурства в команде сервиса. График дежурства прописан в Workplace | Вертикаль/Горизонталь | + | + | + |
Дежурный сервиса способен решать типовые проблемы по инструкции | Вертикаль/Горизонталь | + | + | + |
Описан процесс эскалации для нетипичных проблем | Вертикаль/Горизонталь | + | + | + |
Дежурные получают алерты за свой сервис | Вертикаль/Горизонталь | + | + | + |

## Релизы {#tier-category-releases}
Критерий | Примечание | Тир А | Тир В | Тир С | Тир D
:---: | :---: | :---: | :---: | :---: | :---:
Все события и релизы [передаются](https://wiki.yandex-team.ru/runtime-cloud/nanny/export-to-infra/) в infra/timeline и настроен пресет | Вертикаль/Горизонталь | + | + | + | + 
Полокационная выкладка с подтверждением дальнейшей выкладки после престейбла | Вертикаль/Горизонталь | + | + | + | Приветствуется
Блокирование релизов во время регламентных работ, затрагивающих сервис | Вертикаль/Горизонталь | + | + | + | Приветствуется
Одинаковый порядок релизов зависимых сервисов во всех ДЦ | Вертикаль/Горизонталь | + | + | |

## Работа с инцидентами {#tier-category-incidents}
Критерий | Примечание | Тир А | Тир В | Тир С | Тир D
:---: | :---: | :---: | :---: | :---: | :---:
Работа над инцидентами ведется в очереди SPI | Вертикаль/Горизонталь | + | + | + | +
Команда использует протоколы работы с инцидентами | Вертикаль/Горизонталь | + | + ||
Команда знает про оранжевый и красный протокол | Вертикаль/Горизонталь | + | + | + | +
Процент разобранных SPI - созданы Action Items или выделены SPProblem | Вертикаль/Горизонталь | 80% | 60% | 50% | 
Процент закрытых Action Items | Вертикаль/Горизонталь | 60% | 50% | 40% | 
Есть цель, решающая SPProblem | Вертикаль/Горизонталь | + | | | 
Процент инцидентов c автоматически рассчитанным YDT к общему количеству инцидентов с YDT | Вертикаль/Горизонталь | 75% | 60% | 50% | 
Доля автоматически рассчитанного YDT к общему количеству YDT | Вертикаль/Горизонталь | 75% | 60% | | 
Выполнен SLA на разбор инцидентов (90% инцидентов разбираются за 2 недели) | Вертикаль/Горизонталь | + | + | | 
Процент всех закрытых LSR Action Items | Вертикаль/Горизонталь | 70% | 60% | 50% | 
Доля автоматически рассчитанного YDT к общему количеству YDT | Вертикаль/Горизонталь | 75% | 60% | | 
## Регламентные работы {#tier-category-duty}
Критерий | Примечание | Тир А | Тир В | Тир С | Тир D
:---: | :---: | :---: | :---: | :---: | :---:
Регулярные [прогрузки](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/procedures/proverka-lokacii-na-zapas-v2/) с корректно настроенным таргетом. 70% успешных прогрузок | Вертикаль/Горизонталь | + | + |  | 
Сервис выдерживает -1 ДЦ (По всем инцидентам -1ДЦ должны быть AI, которые должны быть закрыты до завершения ревью периода) | Вертикаль/Горизонталь | + | + | + | +  
Есть регулярные учения по закрытию ДЦ, имеются [автоматические отчеты об учениях в Warden](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/uchenki/dobavitsja-na-dashbord-uchenijj/) | Вертикаль/Горизонталь | + | + | + | 
Есть [сценарий деградации](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/Stabilnyjj-servis/#-eslisluchilosstrashnoe) в случае нештатных ситуаций, либо резкого роста трафика | Вертикаль/Горизонталь | + | | | 
Есть регулярные учения по тестированию сценариев деградации, имеются [автоматические отчеты об учениях в Warden](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/uchenki/dobavitsja-na-dashbord-uchenijj/) | Вертикаль/Горизонталь | + | | | 


## Критерии выполнения целей 9999 {#tier-criteria}
При формировании целей на следующее полугодие команда сервиса выбирает тир надежности, на который она готова сделать закомит.  
Цель считается выполненной, если сервис по итогам полугодия соответствует условиям выбранного тира надежности по указанным выше категориям, либо более высокого тира.  
Каждый сервис сам определяет траекторию движения по тирам надежности.

{% note tip %}

Идеальной траекторией был бы переход в следущий тир надежности каждый год.

{% endnote %}
