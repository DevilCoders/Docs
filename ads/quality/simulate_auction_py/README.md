# Обертка для симулятора
## Из командной строки
Для работы с симулятором из командной строки сделана утилита [ads/quality/simulate_auction_py/scripts/simulate](https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/simulate_auction_py/scripts/simulate)
С помощью нее можно сделать выстрел в симулятор с необходимыми параметрами, зная только идентификатор CTRPredictionID.
Утилиту нужно запускать на машине, на которой есть база `yabsdb` и заресторены нужные таблички: SelectType,
PageGroupExperiment, CTRPrediction и FormulaParameters. Утилита умеет сделать выстрел с заданными параметрами
и запомнить метрики во временном файле, а при последующих выстрелах использовать сохраненные данные для нормировки.
```(bash)
./simulate --host HOST --port PORT etalon-id 7538         # Запустить с параметрами CTRPredictionID=7538
                                                          # Использовать настройки по умолчанию для большого поиска (PageID=2, 3 места в спецразмещении)
                                                          # Записать результаты в файл .etalon.
                                                          # На выходе json с параметрами запуска.

./simulate --host HOST --port PORT simulate-id XXXX       # Запустить с параметрами CTRPredictionID=XXXX
                                                          # Отнормировать, используя данные из файла .etalon
                                                          # На выходе json c отнормированными метриками

./simulate --host HOST --port PORT --override-params "{'premium_params': {'C': 0.2, 'D': 0.5}}" simulate-id XXXX
                                                          # Запустить с параметрами CTRPredictionID=XXXX
                                                          # переопределив необходимые параметры.
                                                          # Отнормировать на данные из файла .etalon

./simulate --host HOST --port PORT --mobile simulate-id 7738
                                                          # Запустить с параметрами CTRPredictionID=7738
                                                          # Использовать настройки для мобильного поиска (PageID in [183,203], 2 места в спецразмещении)

```


## Из ноутбуков IPython/Jupyter
Поскольку в Аркадии не поддерживается IPython/Jupyter, то для работы с утилитой `simulate` из IPython/Jupyter
можно использовать удаленный вызов по SSH. Небольшая дополнительная сложность возникает из-за необходимости правильного
экранирования кавычек при передаче параметров в аргументе `--override-params`. Предлагается использовать такой вариант:
```(python)
from textwrap import dedent

# Шаблон вызова команды ./simulate и подстановка бинарника, хоста симулятора и порта
simulate_command_template = dedent(
    '''
    {binary} --host {host} --port {port} --override-params \"{{override_params}}\" simulate-id 7538
    '''
).strip().format(**{
    'binary': '$HOME/arcadia/ads/quality/simulate_auction_py/scripts/simulate/simulate',
    'host': 'simulator-host-name.yandex.net',
    'port': 1612
})

# Подстановка в команду переопределенных параметров
simulate_command = simulate_command_template.format(
    override_params={"premium_params": {"W": w}}
)

# Экранирование кавычек в команде
simulate_command_quoted = simulate_command.replace('"', '\\"')

# Удаленный вызов через SSH
result_text = ! ssh bsbt00i "{simulate_command_quoted}"

# Парсинг текста ответа в структурированный формат в Питоне
result_dict = eval(result_text[0])
```


# Оптимизация параметров аукциона.
## Введение

Формула value - центральная формула оценки "хорошести" баннера в аукционе. Эта формула имеет вид 
* ` CPMThreshold = -C + D * ctr + E * brel- H * ctr * apc - S * ctr * qrel - T * qrel - U * ctr * brel + W * rp * ctr. `
* ` Value = Bid * CTR - CPMThreshold`
 
В этой формуле ctr,brel,apc,qrel,RP (ReservePrice) определяются прогнозаторами, а коэффициенты C,D,E,F,G,S,T,U мы можем
подбирать, достигая желаемых метрик в аукционе. Их мы называем порогами.

## Как устроен переподбор

В [ads/quality/simulate_auction](https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/simulate_auction) находятся
исходники симулятора, который позволяет по собранному логу реального аукциона, предсказать метрики аукциона
с измененными порогами. Метрики можно посмотреть либо в web-вьюере, либо через апи.

Далее, есть пакет [simulate_auction_py](https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/simulate_auction_py),
который содержит в себе следующие модули:
* интерфейс для обращения к апи симулятора
* модуль для решения параметрической задачи blackbox-оптимизации с несколькими ограничениями
* скрипт [collect-logs-for-simulator](https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/simulate_auction_py/scripts/collect_log_for_simulator),
предназначенный для запуска на нирване графа, подготавливающего логи для симулятора
* скрипт [optimize](https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/simulate_auction_py/scripts/optimize),
предназначенный для работы с оптимизационными задачами (в т.ч. для их запуска на нирване)
* скрипт [simulate](https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/simulate_auction_py/scripts/simulate),
позволяющий получить значение метрик симулятора, используя наперед заданные пороги, вычисляемые на основании
заданного ctr-prediction-id. 

## Как получить oauth-токен и создать secret на нирване?
Чтобы работать с MapReduce на нирване, необходимо положить свой oauth-токен в secret.

* получить oauth-токен [тут](https://auth.qe.yandex-team.ru/). Далее кликнуть по ссылке "+ oauth токен" сверху справа
* [секрет](https://wiki.yandex-team.ru/jandekspoisk/nirvana/vodstvo/rabota-s-sekretami-v-nirvane/) с вашим токеном
-можно создать например через [эту форму](https://wiki.yandex-team.ru/hitman/nirvanasecretsform/)

## Как собрать лог для симулятора?!
Лог для симулятора джойнится регулярно и лежит в yabs-logs/YYYYMM/SimulatorPipeline... 
Тем не менее, для того, чтобы использовать этот лог для симуляций, необходимо отгрепать в нем лишь нужные пейджы,
а также оставить лишь те хиты, в которых не было фрода. Также необходимо заполнитoь и другие нужные симулятору поля.

В простейшем случае все это делает граф на нирване, который можно запустить, например так:
```
./collect-logs-for-simulator --mobile --start-date "2017-01-01T00:00:00" --end-date "2017-01-01T12:00:00" --page-ids 183 --secret "your-secret-here"
```
Обратите внимание на формат даты. Другие форматы не поддерживаются.
Не забывайте указывать --mobile для мобильных пейджей. Это влияет на позиционные CTR.
В более сложных случаях, рекомендуется добавить опцию --draft и уже в интерфейсе нирваны добавить необходимые мапперы,
редьюсеры и постмапперы и запустить граф.
У созданного кубика будет 2 выхода: без применения постмапперов, и - с ними. В стандартной конфигурации
постмапперы используются для того, чтобы оставить только те поля, которые нужны симулятору и уменьшить размер лога.
Лог до постмапперов может быть полезен для дополнительного анализа и проверок.

Простейший пример сбора логов для десктопа лежит тут:
https://a.yandex-team.ru/arc/trunk/arcadia/junk/oleg-pon/CollectLogs/prepare_simulator_log_2.py
Более сложные примеры, где нужно было ремапить линейные модели и применять новые прогнозаторы - тут:
https://a.yandex-team.ru/arc/trunk/arcadia/junk/oleg-pon/CollectLogs/collect_simulator_log_2_rp.py

Важные особенности:
* Метрики BannerSearchRelevance и QuerySearchRelevance являются эталонными и, независимо от выбранного прогнозатора,
используются для подсчета метрик вроде lclicks, pfound,... в симуляторе. А также при проведении аукциона.
* Для того, чтобы pfound считался хорошо, необходимо примапить поле RealRelevanceOfTheFirstPage в RealRelevance лога
для симулятора. Подробнее про pfound [тут](https://st.yandex-team.ru/BSDEV-58026)

## Как запустить симулятор?!

Простой и удобный способ - воспользоваться кубиком [simulate-auction-yt](https://nirvana.yandex-team.ru/operation/bad36663-ea34-11e6-a873-0025909427cc/overview).
В результате, на выходе получится таблица либо с похитовой, либо побаннерной статистикой. Похитовую статистику можно суммировать по интересющим группам баннеров.
Подробнее про парметры этого кубика можно почитать в [ads/quality/simulate_auction_yt](https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/simulate_auction_yt).

Если же лог достаточно маленький, а параметры хочется на фиксировать, а менять интерактивно, то нужно проделать следующее:
Скачиваем [ads/quality/simulate_auction](https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/simulate_auction),
компилируем, собираем лог. 
Копируем все это на одну из машинок tsnet???.search и запускаем как-то так:
```
./simulate_auction -m -l VCG,TrueYAuction -f ~/simulator_pipeline/simulator_pipeline_rp_2_4_0717_0724.tsv -p 1612 -t 31 -k 
```

Важные особенности:
* перед тем, как верить метрикам, полученным в симуляторе, хорошо бы попробовать воспроизвести дефолт, чтобы убедиться,
что лог собран правильно. Для этого нужно скриптом
[simulate](https://a.yandex-team.ru/arc/trunk/arcadia/ads/targeting/yabs-simulate-auction/examples/simulate.py)
"выстрелить" по симулятору параметрами текущего дефолта
``` 
./simulate --host tsnet???.search --port 1612 etalon-id 7208 
```
. В примере 7208 - ctr_prediction_id поискового
дефолта. Далее на результаты можно смотреть браузеров, зайдя на tsnet???.search:1612 Если после этого метрики VCG
аукциона не совпадают с метриками TrueYAuction-а - что-то пошло не так.

## Как решить оптимизационную задачу с помощью симулятора? 

* запустить скрипт optimize как-то так:
```
./optimize -s tsnet???.search -p 1612 -t task.py --task-id FILL_ME_WITH_VALID_TASK_ID> optimization_log.tsv
```
* кстати, optimize info ... можно использовать вместо simulate. Иногда это даже удобней, так как параметры дефолта
можно описать в тексте задачи

## Пример постановки оптимизационной задачи с комментариями

[task.py](https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/simulate_auction_py/scripts/optimize/task_examples/task.py)
- пример задачи здесь будет поддерживаться в актуальном состоянии.
Идея состоит в том, чтобы описать сразу множество почти задач с немного разными ограничениями в одном файле.
Как это делать - понятно из содержимого файла.

## Изменения в связи с переездом на hahn
* В `mapreduce_table` указываем полный путь вместе с `//home/bs`

## Так, а теперь как запустить все это на нирване?!

* запустить ` ./optimize -t task.py run-on-virvana --token TOKEN_HERE`
* после этого будет запущено по графу на каждую из оптимизационных задач
* кстати, токен можно сохранить в переменную окружения NIRVANA_TOKEN
* а еще есть ключ `--draft`, который позволяет лишь создать граф, не запуская его
* все свои графы и их статус можно мониторить на nirvana.yandex-team.ru

## Гарантия в симуляторе

На данный момент в логах симулятора для гарантии хранится не `CTR`, а `CTR*` (см. тикет https://st.yandex-team.ru/BSDEV-61600 ), который используется для отбора. Изначально статистики типа кликов тоже считались по нему, что, очевидно, неправильно.

Для корректной работы с гарантией в симуляторе нужно сделать следующие вещи:

* отгрепать 'плохие' хиты (пример см. [здесь](https://paste.yandex-team.ru/234031))
* добавить в симуляторный лог поле `BKRelevance` (в миллионных долях, как оно есть в SimulatorPipeline!)
* добавить в лог поле TrueGuaranteeCTR, в котором записан настоящий CTR (**опционально**)

Логика работы для гарантии следующая:

##### Подсчет статистик

- Если есть полe 'TrueGuaranteeCTR', то все статистики вычисляются по этому полю
- Если поля 'TrueGuaranteeCTR' нет, то обратное преобразование `CTR* -> CTR` делается внутри симулятора, согласно параметрам `Stat_A`,`Stat_B`,`Stat_C`, `Stat_Threshold` 

##### Отбор объявления

Здесь ключевая функция GetCTR

- Если поля `TrueGuaranteeCTR` нет, то используется поле `CTR` из лога (в нем записан движковый `CTR*`)
- Если есть полe `TrueGuaranteeCTR`, то внутри симулятора выполняется преобразование `TrueGuaranteeCTR -> CTR*` согласно параметрам `A`,`B`,`C`,`Threshold` и полю `BKRelevance`. Здесь так же есть возможность использовать кастомную релевантность. Для этого нужно записать свою релевантность в поле `BannerSearchRelevance{1,2,3,4}` и указать это в структуре `CustomField` веб-интерфеса.



Таким образом, если у вас нет цели подобрать новые параметры, новую релевантность или новый `CTR` для гарантии, то добавлять поле `TrueGuaranteeCTR` не нужно. Достаточно добавить поле `BKRelevance` и убедиться, что выставлены актуальные параметры. В этом случае отбор объявлений будет производиться по значению `CTR*`, записанному в логе, а для подсчета статистики будет делаться обратное преобразование.

##### Что за параметры?

 `A`,`B`,`C`,`Threshold`,`Stat_A`,`Stat_B`,`Stat_C`, `Stat_Threshold`
На данный момент эти параметры **не обновляются при стрельбе**, а просто захардкожены. Их актуальность можно проверить в таблице Relevance (`A`,`B`,`C`,`T`)

##### Ничего не понятно?

borislav@ проводил эксперименты с гарантией и разбирается в работе симулятора 

## Существующие проблемы
* Если на почту приходит пустой лог, и письмо [SUCCESS] от нирваны, то значит скорее всего что-то не так с кубиком
на нирване. oleg-pon@, vechkasova@ умеют в этом разбираться

