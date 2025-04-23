# Факторы по запросным классификаторам [WizDetection](https://a.yandex-team.ru/arc/trunk/arcadia/search/begemot/rules/wiz_detection)

WizDetection - правило в Бегемоте, вычисляющее предсказания классификаторов на запросе. Подробнее можно почитать [тут](https://a.yandex-team.ru/arc/trunk/arcadia/search/wizard/data/fresh/WizDetection/README.md).

Предсказания запросных классификаторов могут быть полезны как факторы для обучения формул.
Этот калькулятор протягивает `Probability` из результата бегемотного правила WizDetection в [динамические факторы Блендера](https://wiki.yandex-team.ru/JandeksPoisk/KachestvoPoiska/Blender/features/dynamicfactors/).

Динамические факторы лежат в Source [`wizdetection`](https://a.yandex-team.ru/arc/trunk/arcadia/yweb/blender/lib/dynamic_factors/descriptor.h?rev=4721097#L32), с ключом, который задается в специальном конфиге [wizdetection.factors.json](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrs_upper/rearrange.dynamic/blender/wizdetection.factors.json) из rearrange.dynamic.

#### Формат конфига и как добавить свои факторы

Добавление в конфиг `$key : [$name1, $name2]` добавит вероятности предсказания классификаторов с Name `$name1`, `$name2`, которые обязательно должны содержаться в конфиге [быстрых данных WizDetection](https://a.yandex-team.ru/arc/trunk/arcadia/search/wizard/data/fresh/WizDetection/formulas_new.pb.txt)

Формат достаточно простой, достаточно посмотреть на соседние ключи.

#### Где посмотреть как это работает

В ([куке релевантности](https://wiki.yandex-team.ru/jandekspoisk/panelupravlenija/pravilakuki/) &rarr; Компоненты релевантности) в левой колонке можно найти правило `WizDetection` и его предсказания.

В (куке релевантности &rarr; ApplyBlender &rarr; dynamic_factors) можно увидеть как они пробрасываются в динамические факторы.

### FAQ

> Почему бы не добавить для каждого классификатора свой ключ, зачем вообще нужен конфиг?

Делать ключи, содержащие одно значение, это не очень хорошая практика. 
При обучении блендерных формул нужно будет указывать много полей (`wizdetection.ya_health_drugs.0-0`, `wizdetection.ya_health_med_query.0-0` ...).
Плюс далеко не всем нужны классификаторы в качестве факторов. 
 
> Почему бы не сделать ключ, содержащий все классификаторы?

Классификаторы появляются и удаляются. Некоторые из них служат исключительно для событий (выборы мэра Москвы, ЧМФ 2018).
Это приведет к тому, что будет куча нулевых факторов, и ссылки на ныне несуществующие классификаторы.

> Что делать если классификатор нужно обновить?

Лучше сделать дублирующий классификатор и создать новый ключ, переключиться на него и потом удалить старый.
