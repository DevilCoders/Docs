Таск представляет из себя yaml-файл, в котором в разных его секциях описаны настройки различных этапов обучения формулы.
Типичный таск содержит секции
[calc или calcs](#calcs) для описания мапперов, которые надо применить к входным таблицам.
[preprocessors](#preprocessors) для описания препроцессоров, которые надо применить к входным таблицам.

# Предобработка
## Map-предобработка <a name="calcs"></a>
В этой секции описывается цепочка мапперов, которую мы применяем ко входу.
Частично схема описаны в [протобуфе](https://a.yandex-team.ru/arc/trunk/arcadia/ads/ml_engine/protos/calc.proto)
Работает это так, что все эти мапперы группируются один за другим и все вместе выполняются в одной map-операции.

Секция `calcs` представляет из себя словарь, в котором ключи -- произвольные строки, а значения должны подходить под 
[TCalcDescription](https://a.yandex-team.ru/arc/trunk/arcadia/ads/ml_engine/protos/calc.proto#L27), которые могут создавать произвольного вида мапперы.
В текущем виде это могут быть [TArbitraryMappers](#arbitrary_mappers) и [TApplyLM](#apply_lm).
Cекция `calc` более простая, она должна подходить под [TArbitraryMappers](#arbitrary_mappers) и ее содержимое попадает в `calcs` с ключом "".
Все мапперы из секции `calcs` склеиваются в список в порядке лексикографической сортировки ключей и так применяются.

### Произвольные мапперы <a name="arbitrary_mappers">
Схема описана в протобуфе в классе [TArbitraryMappers](https://a.yandex-team.ru/arc/trunk/arcadia/ads/ml_engine/protos/calc.proto#L2).
Работает это так, что выполняется то, что написано в `exec`, после этого результат `eval(mappers)` воспринимается как список mapper-ов, которые надо выполнить.
В начале исполнения каждой джобы операции, исполняющей этот код, будет выполнен код, находящийся в begin в неймспэйсе модуля `yabs.tabtools`,
обычно begin используется для инициализации чего-то, что потребуется при исполнении кода, переданного как строка в классы Mapper, Grep, Split.

### Применение линейной модели <a name="lm_apply">
Схема и немного комментариев есть тут: [TLMApply](https://a.yandex-team.ru/arc/trunk/arcadia/ads/ml_engine/protos/calc.proto#L10)
Если выбран `lm_apply`, то будет применена линейная модель. Результат пойдёт в поле, которое конфигурируется через `target_field`, поиск дампов с моделями задаётся через `task_id`.
В случае обычного применения надо еще задать `last_log_date`, в случае спирального он выберет даты сам, но нужно указать колонку со временем в логе и оционально задержку во времени.

## Произвольная предобработка одного лога <a name="preprocessors"></a>
Структура секции `preprocessors` такая же, как и в [calcs](#calcs), ключи -- произвольные строки, значения -- 
[TPreprocessorDescription](https://a.yandex-team.ru/arc/trunk/arcadia/ads/ml_engine/protos/calc.proto#L39).
Сейчас поддерживается только `TArbitraryPreprocessor`, который работает так, что запускается то, что написано в `exec`, а потом тот объект, который возвращает
`eval(preprocessor)` рассматривается как
[BasicPreprocessor](https://a.yandex-team.ru/arc/trunk/arcadia/ads/libs/py_ml_factors/ml-factors/py-modules/matrixnet/learn_preprocessors.py?blame=true&rev=4043211#L221)
у которого process_logs выдаст таблицу с результатом препроцессора.

# Примеры разных фичей
- [Множественные calcs и preprocessors](https://a.yandex-team.ru/arc/trunk/arcadia/ads/ml_engine/tasks/experiments/mstebelev/eshows_as_factor/cpm.yml?rev=4043211&blame=true)
