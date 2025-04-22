=== Бенчмарк ExamineQueries

Замеряет время, затраченно на ExamineQueries для переданного набора профилей

=== Как собрать корпус профилей для теста

Перед вызовом ExamineQueries [тут](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/shard_processor/shard_processor.cpp?rev=4607005&blame=true#L356) нужно вставить примерно такой код:

```C++
{
    TOFStream fOut("path/to/protos/" + ToString(profile.ProfileId));
    profile.GetProtos().Save(&fOut);
}
```

Перед запуском бенчмарка необходимо скачать базы для InfoKeeper-а и подготовленные на прошлом шаге профиля. Для этого надо запустить bash скрипт load_bases.sh (если были собраны новый профиля, то в скрипте нужно обновить id ресурса с базами перед запуском)
