
# Задачка [VSML-645](https://st.yandex-team.ru/VSML-645)

 - [index.ipynb](./index.ipynb) - собираем данные для разметки в [merge.csv](./merge.csv)
 - [check.ipynb](./check.ipynb) - проверяем новые проврки по метрикам
 - повышаем качество матчинга [тут](https://yql-beta.yandex-team.ru/Operations/YFJTMSyLNU_oZV9wj5mFvoO-3cmEd3-RzrT6p2gcpvc=) `data/yt___home_verticals_.tmp_tmp_2dd463d0_88216e89_6ef0c47d_a4649dca`
 - собираем как было раньше [до этого](https://yql-beta.yandex-team.ru/Operations/YBxZfyyLNT3XEyn2YTcFNB3DE8_lhgcrv-C2LPkgA54=?editor_page=main) в файлик `data/without_yt___home_verticals_.tmp_tmp_44fa6030_5703291a_a0f8779_4942c699`

![Schema X-Mind](x-mind.png)

## Данные

- [dopel matched](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/doppel/prod/warehouse/auto/matched_offers)
- [yql offers 400](https://yql-beta.yandex-team.ru/Operations/YFNyyL94hu1QGcVa01dQFGoGjNth0R9UrVycrbmeWfg=)
- [original](https://yql-beta.yandex-team.ru/Operations/YFNwIwPTThjUoTaS-PYFKhII8ejDRzTJlquv7f4VwnM=), [impruved](https://yql-beta.yandex-team.ru/Operations/YFN5TAPTThjUoUOVst6ivfJnFU92uIXg7bZehPvh72o=) doppel

## Результат

Очень хочется верить, что удалось повысить precision до 90%, а recall до 97%

|      |   было |   стало |
|:---- | ------:| -------:|
| precision  |  81,7% |  89,2% |
| recall  |  94,1% |  97,2% |


- [merge.xlsx](https://nda.ya.ru/t/0bL338qG3nKbmN)
- [result.xlsx](https://nda.ya.ru/t/FtKH07wf3qADRG)

### Какие гипотезы не плохо себя показывают

1) В тех параметры добавить `year`, `engine_type`, `transmission` и `horse_power` или `displacement` оба последних у нас плавают
2) Убрать из матча по параметрам цвет (с ним обнаружена беда)
3) Добавить к окончательному матчингу сравнение не только по % но и по округлению
4) Матчить по картинкам только если price или mileage сходятся, а картинки похожи на 99% и более
5) по тех параметрам матчить если цвет сходиться

### Изменения

тут https://yql-beta.yandex-team.ru/Operations/YF2z7dK3DKODWsQBxGtsjLdZJhHprnft6NU5RCrhNSY=


### Ограничения

Ещё, поводу старых результатов, они брались для %%recall_timestamp is not null%% что не совсем корректно

Можно косвенно оценить качество склейки по тому сколько раз мы склеиваем один наш оффер с офферами на авито

берем 2021-03-15, там 131842 офферов склеенных с авито из них только 120622 имеют уникальный main_id

То есть не правильно склеенных не менее 11220, а скорее всего больше, предположим в 2 раза, потому что ошибка есть как в одну так и в другую сторону (скорее всего она ещё больше, потому что были найдены и устранены другие факторы вкладывающие свою ошибку)

то есть precision вряд ли был более 83% (131842-2*11220)/(131842)
после исправления ошибок в разметке precision=79%, что соответствует ожиданиям

### Обнаруженные проблемы

<img src="https://79.img.avito.st/1280x960/10674236079.jpg" height="200" align="right" style="margin-left: 20px;float: right;" />

1. Если у нас и на авито цвет Бежевый, то цвета выставляются разные #C49648 и #FAFBFB
2. `displacement` и `horse_power` плавают, вместо сравнения по одному приходиться сравнивать их обоих, чтоб вероятность сходимости была больше, но не уверен что она становится 100%
3. Иногда мы сравниваем формы и всякие другие не машины:
   - `https://79.img.avito.st/1280x960/10674236079.jpg`
   - `http://avatars.mds.yandex.net/get-autoru-vos/2125735/097cb5be4b4cc553cb6fc725db7e60d5/1200x900`
надо добавить в комп зрении предикат, есть машина на фото или нет


