## Описание
Программа для выгрузки GPS треков, записанных в YaWay, из трекера, и сохранения
их в виде таблиц на YT.

Тикеты в очереди должны иметь название вида `<name> BY <email>`, иметь одно
вложение с mimetype=`application/x-protobuf`.

У созданных таблиц создаются аттрибуты `author` и `description`.
`author` - не автор тикета, а то, что написано после "BY" в summary.
`description` - описание в тикете. Это тот текст, который пользователь может
набрать в приложении перед отправкой, а также информация об устройстве, которую
дописывает библиотека recording (UUID, Device Id, User agent).

Если в `description` первая строка (комментарий самого пользователя,
без информации об устройстве) имеет вид `vehicle_type route`, то в созданной
таблице появятся столбцы `vehicle_type` и `route`. Если же комментарий
не в таком формате, таблица создаваться не будет и тикет закрываться не будет.
Вместо этого появится warning о формате комментария.
