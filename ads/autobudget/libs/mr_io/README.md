# Библиотека для работы с входными и выходными данными для map-reduce вычислений на С++

Содержит в себе **ads/autobudget/libs/mr_io**:
* **struct_generator.h** - позволяет определить структуру, содержащую необходимые поля с заданными типами
* папки **yt** и **yql**, в каждой из них:
  * **../interface.h** - оборачивает входной и выходной поток в ```TReader<TInputRecord>```, ```TWriter<TOutputRecord>```, понятный для редьюсеров интерфейс
  * **../converter_header.h** - объявляет функции ```From/To YTNode``` для yt и ```From/To UnboxedValue``` + структура ```TInfo```
  * **../converter_impl_generator.h** - предназначен для генерации реализаций функций, описанных в converter_header.h

Для определения поля используется:
* ```FIELD(NAME, TYPE)```/```OPTIONAL_FIELD(NAME, TYPE)```
* ```FEATURES_FIELDS(NAME, TYPE, FEATURE_NAMES)``` - ```THashMap```  содержащий поля FEATURE_NAMES типа TYPE, ```From YTNode/UnboxedValue``` не реализовано.

Строковый тип не реализован, можно добавить по аналогии с ```OPTIONAL_FIELD```.

Примеры структур и converter-ов: [action_model](https://a.yandex-team.ru/arc/trunk/arcadia/ads/autobudget/action_model/libs/reducer_io).
