## Быстрые данные правила [WizDetection](https://a.yandex-team.ru/arc/trunk/arcadia/search/begemot/rules/wiz_detection)

Правило WizDetection применяет Catboost-, VowpalWabbit-, NeoCortex- и линейные классификаторы. Результатом являются "вероятность" (число в отрезке [0;1]) и результат классификации (false/true). Примеры работы в проде можно найти в куке релевантности -> WizDetection.

Чаще всего используется для определения показа колдунщика / похода на источник. Однако, вы можете использовать их и для своих целей.

### Признаки

Возможными признаками классификаторов на текущий момент являются следующие сущности:

1) Dssm-эмбеддинги, рассчитанные по normalized request. 
Чтобы понять, какие типы эмбеддингов сейчас поддерживаются, нужно посмотреть в поле EDssmEmbedding в [proto-файлике](https://a.yandex-team.ru/arc/trunk/arcadia/search/begemot/rules/wiz_detection/proto/wiz_detection.proto)
или в код [dssm_base.h](https://a.yandex-team.ru/arc/trunk/arcadia/search/begemot/rules/wiz_detection/dssm_base.h). Используется в Catboost и в линейных моделях.

2) Нормализованный запрос. Нужно для VowpalWabbit- и NeoCortex- моделей.

3) Результаты работы других классификаторов. Вероятность можно заиспользовать как признак. Нужно для создания ансамблей.
Часто делают разнордные ансамбли вида 0.7 * catboost_pred + 0.3 * vowpal_wabbit_pred

## Опции классификатора

### Name

Основной идентификатор классификатора. Является уникальным. Иначе UB

### Threshold

Порог для срабатывания классификатора. Если этот порог <= 0.0 или >= 1.0, то формула считается выключенной и не вычисляется.
Для отключения порога можно использовать малые числа, например `0.0000000001`

### Updated

timestamp заливки

### Feature

Множественный параметр, перечисляющий тип фичей. Необязательное поле. Возможные значения
- `Dssm` (пока что только Multiclick)
- `FormulaPrediction` - Name другой модели, её Probability; используется для ансамблей)
- `Query` - чистый запрос как текст (для `.vw` моделей)

### Sigmoid

Флаг применения сигмоиды к результату. Необязательное поле. Возможные значения:
- `true`
- `false`
При отсутствии флага сигмоида <b>применяется</b>

### LogRawProbability

Флаг для безусловного логирования результата классификатора в rearr с значением `wizdetection_Name_prob`, где `Name` идентификатор классфикатора. Необязательное поле. Возможные значения:
- `true`
- `false`
При отсутствии флага логирование именно этого поля выключено.

### ModelPath

Имя файла модели. Сам файл должен быть описан в ya.make или находиться внутри папки
Тип модели определяется по расширению файла

#### Catboost
Если файлик заканчивается на `.cbm`, то это катбуст-модель. Модель стандартная катбустовая. 

В нирване есть кубик для обучения такой модели на dssm-эмбеддингах [Train catboost query embed classifier](https://nirvana.yandex-team.ru/flow/812a48ad-724c-4d76-87ff-b751c20997a7/40b2d5c3-6b27-41df-bec0-f1f4d8b658b0/graph/FlowchartBlockOperation/4d851383-466a-479d-841b-53b372263f7d)

Пример обучения catboost-классификатора можно увидеть [в этом графе](https://nirvana.yandex-team.ru/flow/812a48ad-724c-4d76-87ff-b751c20997a7/40b2d5c3-6b27-41df-bec0-f1f4d8b658b0/graph)

#### VowpalWabbit
Если на `.vw`, то это VowpalWabbit. Модель отличается от той, что генерирует стандартный vw.

Для того, чтобы перевести классическую vw модель в нужный формат, в Нирване есть два кубика [vw_convert_model_to_readble_model](https://nirvana.yandex-team.ru/operation/46e0b2b8-0bbd-484f-b788-6fa8845c3c94/overview) и [vw_convert_readable_model](https://nirvana.yandex-team.ru/operation/d610be4a-d63d-4fe5-91b8-5a0cca498ab9/overview). 
В качестве кубика, который полностью обучает модель и выдает ее в нужном формате, можно брать [learn VW query classifier](https://nirvana.yandex-team.ru/operation/b66dfc9a-188b-4536-8658-7b7cb76e0946/overview).

Пример обучения vw-классификатора можно увидеть [в этом графе](https://nirvana.yandex-team.ru/flow/774eaf74-7358-4a92-b1f4-9f8cfbc09153/6b5950ed-3c9b-4931-b652-6b4f6fc43e1b/graph)

#### NeoCortex
Если на `.nx`, то это NeoCortex-модель. Представляет собой бинарный файл, генерируемый обучалкой neocortex'а.

Документация neocortex'а находится [тут](https://a.yandex-team.ru/arc/trunk/arcadia/ml/neocortex).
Обратите внимание, что для однообразности к результату neocortex'а **не добавляется** априорная вероятность и применяется сигмоида,
поэтому результаты будут отличаться от стандартных неокортексных примеров использования.

Графа обучения неокортекса нет, зато есть ~~рисунок графа~~ [комментарий](https://st.yandex-team.ru/SPORTSERP-310#5d2d96c463890d001d895193) в ST от wd28, как можно обучить такой классификатор. Если сделаете граф, дайте мне знать.

#### Линейная модель 
Если на `.lm`, то это линейная модель вида $a_0 + a_1 \cdot f_1 + a_2 \cdot f_2 + \ldots + a_n \cdot f_n$.

Линейная модель полезна, если вы решили сделать логарифмическую регрессию над dssm.
Представлена json-файлом со следующими полями:
- обязательное поле `coeffs`- array of float, коэфициентов, на которые домножаются признаки ($a_1, a_2, a_3 \ldots a_n$)
- необязательное поле `const` - float, свободный коэфициент модели ($a_0$, $default=0$)
- необязательное поле `sigmoid` - bool. Если false, то к результату не применяется сигмоида.
- необязательное поле `clampval` - bool. Если false, то результат <b>не</b> обрезается снизу 0.0 и сверху 1.0.
- необязательное поле `log_raw_probability` - bool. Если true, то результат модели безусловно логируется в rearr `wizdetection_Name_prob`, где `Name` имя модели.
<b>ВНИМАНИЕ</b> поля модели `sigmoid`, `clampval`, `log_raw_probability` перезаписывают соответствующие настройки из конфига модели (при наличии).

Графов с "обучением" модели нет, но есть [граф с применением лин.модели](https://nirvana.yandex-team.ru/flow/c8a45df3-50c2-45b3-999a-c20bb9db8fec/0e8c3302-c8b3-4c26-af58-8bb9d3d92588/graph/FlowchartBlockOperation/35bc801a-91d0-47e5-8d0f-84cc721cf429) к результатам vowpal wabbit и catboost.
Линейные модели коммитятся вручную (не в sandbox).

### formulas_new.pb.txt
formulas.pb.txt - старый файл. С момента релиза [Begemot 289](https://st.yandex-team.ru/BEGEMOTREL-157), все формулы переезжают на formulas_new.pb.txt

Формат formulas_new.pb.txt определяется [proto-файлом](https://a.yandex-team.ru/arc/trunk/arcadia/search/begemot/rules/wiz_detection/proto/wiz_detection.proto).
Все файлы, кроме `.lm` моделей подтягиваются из Sandbox'a.

## Как добавить новый классификатор

Легкий путь и правильный путь:

Воспользоваться инструкцией [Добавить классификатор](https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/blender/query-classifiers-101/)
Он умеет коммитить Catboost и VowpalWabbit классификаторы
[Пример графа с коммитом катбуста](https://nirvana.yandex-team.ru/flow/812a48ad-724c-4d76-87ff-b751c20997a7/40b2d5c3-6b27-41df-bec0-f1f4d8b658b0/graph)
[Пример графа с коммитом VW](https://nirvana.yandex-team.ru/flow/774eaf74-7358-4a92-b1f4-9f8cfbc09153/6b5950ed-3c9b-4931-b652-6b4f6fc43e1b/graph). Обратите внимание, из какого выхода обучающего кубика необходимо подавать модель для коммита.

Сложный путь (и пока что единственный для `.lm` и `.nx`):

1) Убедиться что классификатор имеет нужное расширение файла и залить в Sandbox `ya upload --ttl=inf <filename>`, если это catboost/vw/nx модель. Либо закоммитить модель в эту папку, если это `.lm` модель.
2) Добавить модель в ya.make <b>в 2 местах</b> - FROM_SANDBOX и COPY
3) Добавить описание модели в formulas_new.pb.txt

[Пример коммита](https://a.yandex-team.ru/review/924667/files/1)

Классификатор доедет до прода с ближайшим [релизом быстрых данных бегемота](https://sandbox.yandex-team.ru/tasks?type=RELEASE_BEGEMOT_FRESH)

## Кросс-ссылки на вики
- [Детальное техническое описание классификаторов](https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/blender/classifiersnotes/)

## Ответственные
- [Блендер](https://abc.yandex-team.ru/services/blndr/)
