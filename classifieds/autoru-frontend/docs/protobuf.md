# protobuf

Используем [protobuf-ts](https://github.com/timostamm/protobuf-ts)

На данном этапе внедрения компилируем proto-файлы при сборке проекта.
Если все будет хорошо, то этап сборки можно будет унести в [schema-registry](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/publish/compile_ts.sh)
и поставлять в npm-пакете уже собранные файлы.

На данный момент мы не можем использовать сгенерированные типы `protobuf-ts` из-за [проблемы](https://github.com/timostamm/protobuf-ts/issues/137).

## Общая схема работы

* Оригинальные proto-файлы храняться в репе [schema-registy](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto)
* Мы получаем их в npm-пакете `@vertis/schema-registry`
* В make есть цель `protobuf-ts`, которая компилирует в TS нужные нам файлы. Скомпилированные TS-файлы находятся в `auto-core/proto/compiled`. Не надо добавлять их в репу.
* Скомпилированные файлы надо добавлять в общий реестр `auto-core/proto/schema-registry.ts`, чтобы они были загружены

## Типичные проблемы

* Если при запросах в бек получается ошибка `no such type XXXXX`, это значит, что наш код не знает по этот тип сообщения. Надо сделать 3 вещи:
  1. Найти файл, где лежит это сообщение в репе [schema-registy](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto)
  2. Добавить этот файл в [make сборку](https://a.yandex-team.ru/arcadia/classifieds/autoru-frontend/Makefile#L25)
  3. Добавить этот файл в [загрузку в JS](https://a.yandex-team.ru/arcadia/classifieds/autoru-frontend/auto-core/proto/schema-registry.ts#L9)
* Если при запросах в бек получается ошибка декодирования или вы результирующем JSON отсутствуйте какое-то новое поле, то обнови npm-пакет `@vertis/schema-registry`

## Про скорость

protobuf на больших и сложных моделях (например, листинг) медленнее, чем JSON.

[Синтетический тест](https://a.yandex-team.ru/arcadia/classifieds/json-vs-protobuf):
```
benchmarking auto.api.OfferListingResponse decode+toObject (protobuf payload 170904) performance ...

protobuf.js (compiled) x 429 ops/sec ±3.89% (90 runs sampled)
JSON.parse x 543 ops/sec ±0.76% (89 runs sampled)

JSON.parse was fastest
protobuf.js (compiled-strip) was 17.5% ops/sec slower (factor 1.2)
```

Но выигрыш мы получаем за счет того, что public api отвечает быстрее в pb.
И медленное декодирование pb в nodejs нивелируется ускорением ответа public api.
[Графики TTFB и полного времени ответа для листинга](https://st.yandex-team.ru/AUTORUFRONT-15169#60e9c9c933792e40f9cdebc8)

## Сравнение вариантов

Есть несколько быстрых реализации работы с protobuf в JS. Гугловую не рассматриваем, она очень медленная.

Требования: public-api отдает JSON согласно [canonical proto3 JSON format](https://developers.google.com/protocol-buffers/docs/proto3#json) +
необходима поддержка опции `json_write_default_value` для добавления дефолтных значений полей (согласно декларации сообщения) в ответ.

[**protobufjs**](https://github.com/protobufjs/protobuf.js):
* (±) компилит все в один файл
* (±) умеет делать d.ts
* (+) умеет по флагу не генерировать дефолтные значения у полей
* (-) есть плохой баг с зависимостями. Из-за него сейчас не получится использовать pb для Гаража и VIN-отчетов.
* (-) плохо развивается
* (-) не поддерживает кастомные опции

[**ts-proto**](https://github.com/stephenh/ts-proto)
* (±) компилит все в отдельные файлы в той же структуре, что и оригинальные `*.proto`
* (±) сразу генерирует `.ts`
* (+) может генерировать типы как camelCase, так и snake_case
* (±) под капотом использует pbjs
* (+) работает поверх оригинального protoc, поэтому нет бага с зависимостями
* (-) для всех полей всегда отдает дефолтные значения. Конкретно нам это мешает в листинге, т.к. там ссылки строятся по текущим фильтрам поиска,
  а дефолтные поля провоцируют там кучу мусора. По той же причине ломается счетчик количества фильтров.
  Плюс ко всему `0` и дефолтное значение не отличимы друг от друга, что проводит к багу с дефолтами `?price_from=0&price_to=0` - всегда отдает пустой поиск.
  В теории, можно придумать историю по вычитанию дефолтов из результата декодирования pb.
* (+) развивается
* (-) не поддерживает кастомные опции

[**protobuf-ts**](https://github.com/timostamm/protobuf-ts)
* (±) компилит все в отдельные файлы в той же структуре, что и оригинальные `*.proto`
* (±) сразу генерирует `.ts`
* (-) может генерировать типы только camelCase (дефолтный вариант в canonical proto3 JSON format), но умеет сериализовывать в snake_case тоже
* (+) работает поверх оригинального protoc, поэтому нет бага с зависимостями
+ (+) умеет canonical proto3 JSON format
* (+) развивается
* (+) поддерживает кастомные опции. Не хорошо и удобно, но `json_write_default_value` сделать можно.

## Баг с зависимостями protobufjs

pbjs неправильно резолвит импортируемые сообщения.
Из-за этого поле `mark_logo` в [auto.api.vin.PtsBlock](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/auto/api/vin/vin_report_model.proto#L153) становится
[auto.api.vin.Photo](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/auto/api/vin/common.proto#L17),
а должен быть [auto.api.Photo](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/auto/api/common_model.proto#L180)

Как должно быть. Резолвинг должен сначала искать внутри текущего файла/сообщения, если таких сообщений нет, то строго только внутри импортируемых файлов. Если и там нет, то выдавать ошибку.
Так работает ванильный protoc.

pbjs строит полное дерево всех классов и ходит вверх-вниз не по импортируемым файлам, а по всему дереву. Т.о. согласно правилу "сначала ищем внутри, потом снаружи", получаем неправильный резолвинг `mark_logo`.

## Как обновлять или менять библиотеку

После изменений надо выкатить брач в shiva и пострелять.
Примеры стрельб и патроны есть в [Лунапарке](https://lunapark.yandex-team.ru/AUTORUFRONT-15169), дашборды и графики в [таске](https://st.yandex-team.ru/AUTORUFRONT-15169).
Нам интересны TTFB (время получения от бека первого байта ответа) и общее время ответа (по сути это TTFB+декодирование protobuf внутри nodejs).
