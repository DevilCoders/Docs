### Матрикснет для геноцида

#### Фичи, их извлечение

Фичи перечисляются в ads/bsyeti/libs/cleansing/proto/cleansing.proto в TProfileCleansingFeatures

Каждая фича имеет уникальные аттрибуты NYT.column_name, MxPosition.

На данный момент основные фичи:
- HasKeyword{keyword} - есть ли в поле UserItems киворд keyword
- Has{Field} - есть ли поле field из profile.proto
- Size{Field} - размер поля field из profile.proto


#### Пайплайн обучения

На старте у нас есть таблица с профилями Profiles.

В конфиге cleansing_new указывается путь до таблицы Profiles и beh-profile-hit-log лога.

Затем запускается cleansing_new. На выходе получается таблица Trainset.

Запускается prepare_task для автогенерации конфига матрикнета. В конфиге генератора нужно указать путь до Trainset.

Собирается ads/ml_engine/tool и запускается с полученным конфигом.
ya m ads/ml_engine/tool && ./ads/ml_engine/tool/ml_engine path_to_task
