## YT RAW History

В данном слое хранится история изменений документов в формате [RAW](generated-targets.md#raw).
Она должна быть неизменяема, поэтому старые партиции репликация сжимает в специальном режиме `rotate_policy: raw_history`.

В этом режиме репликация идет по изменяемому полю (вида updated), которое также является ключевой колонкой в YT RAW таблице
идущей на первом месте. Для иммутабельного поля (вида created) история изменений, как правило, не имеет смысл,
потому этот режим обычно не ставится.


### Переинициализация
Статические таблицы будут скипаться при записи в них. По умолчанию динамическими будут оставаться только таблицы за 3 последних дня для партицирования по дням, за 1 месяц и за 1 год для партицирования по месяцам или годам.
В случае [перегрузки](faq.md#reinit), то есть, при выполнении `init` правила с выставлением даты на уже включенное правило, все партиции, начиная с этой даты, будут сделаны динамическими и в них будут попадать обновления.

{% note warning %}

Для перегрузки вам нужно указать в драфте минимум 2 таргета: из источника в queue_mongo, и из queue_mongo в YT raw_history

{% endnote %}

{% note warning %}

Обычный init не приведет к перегрузке истории, если таблицы уже статические. В этом случае их можно удалить руками отдельно

{% endnote %}

### Сжатие старых партиций

#### Зачем это нужно
Квотируемыми ресурсами в YT являются:
* Ноды
* Таблеты
* Чанки
* Место на диске

Путем сжатия мы не можем контролировать количество нод, но все остальное — можем.
Для сжатия по дефолту используем `compression_codec='brotli_8'`, `erasure_codec='lrc_12_2_2'`.
Они дают максимальное сжатие, но при длительном времени работы.
Подробнее про erasure кодирование можно почитать [тут](https://yt.yandex-team.ru/docs/description/common/replication?),
про алгоритмы сжатия в YT - [тут](https://yt.yandex-team.ru/docs/description/common/compression?).

#### Пул для сжатия
Чтобы сжатие работало корркетно, стоит указать пул для вычислительных операций в YT.
Выставляется в `plugins/config.yaml` вашей группы правил, пример:
```
yt:
    raw_history_pool:
        production:
            hahn: pool1
            arnold: pool2
```
Чтобы был доступ, нужно выдать роль `use` на указанные пулы роботам соответствующих окружений: {{ yt_replication_robots }}.


#### Выбор партиций для сжатия
Партиции для сжатия у таргета выбираются следующим образом:
* Проверяем, что у данного таргета есть партицирование и у него `rotate_policy: raw_history`
* Собираем все динамические партиции для таргета
* Выбираем те, которые находятся в неактивных партициях - все, что раньше партиции, в которую сейчас
реплицируются данные за исключением `items_to_keep` следующих за ней партиций (по дефолту для raw_history `items_to_keep = 2` для
партицированных по дням таргетов, в остальных случаях `items_to_keep = 1`)
* Сравниваем дату партиций с датой последнего отреплицированного документа таргета - она должна
быть меньше (то есть в эти партиции репликация больше не пишет данные)

Все выбранные таким образом партиции будут сжаты.

#### Как происходит сжатие партиции
Этапы сжатия партиции:
1) Репликация отмонтирует таблицу и берет на нее эксклюзивный лок на изменения
2) Создастся временная статическая партиция с такой же схемой, что и исходная
3) Запустится операция `merge` динамической таблицы с созданной статической
4) Репликация подменит исходную динамическую партицию созданной статической - она окажется там, где
изначально была динамическая

Посмотреть кроны сжатия можно в [админке](https://tariff-editor.taxi.yandex-team.ru/dev/cron?service=replication&name=yt_rotate_raw_history)
