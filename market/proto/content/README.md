## Что это?

Большая библиотека протобафов, использующихся в разных проектах.
Раньше жила в [гитхабе](https://github.yandex-team.ru/market-java/market-proto), затем по частям разъехалсь по аркадии.

## Нюансы использования

* При добавлении нового прото файла, не забудьте прописать его в ya.make
* При использовании из гитхаба, нужно после пуша сделать релиз, после чего библиотека попадет в артифактори.
  Номер релиза будет новой версией, после чего либу можно подтянуть через гредл. Релизные машины:
    - [market-proto-arcadia](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/market-proto-library)
    - [market-proto-arcadia-jetty6](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/market-proto-library)
* Стоит учитывать, что для сборки используется дефолтная для аркадии версия protobuf (3.17.3 на данный момент)
* Некоторые протобафы из гитхаба не попали в эту большую библотеку и были разнесены ближе к потребителям

## Особенности сборки

* Для генерации сервисов\стабов используется самописный [protobuf плагин](https://a.yandex-team.ru/arc_vcs/market/proto/mbo/mbo-protoc-plugin) (marketrpc),
а также библиотеки вспомогательных классов [market-proto-java](https://a.yandex-team.ru/arc_vcs/market/proto/mbo/market-proto-java) для jetty9 и [market-proto-java-jetty6](https://a.yandex-team.ru/arc_vcs/market/proto/mbo/market-proto-java-jetty6) для jetty6
* market-proto также содержал тулзу для чтения протобуфных файлов [java-pbcat](https://a.yandex-team.ru/arc_vcs/market/jlibrary/market-proto/java-pbcat) и отдельную библиотеку с вспомогательными классами [protobuf-handlers](https://a.yandex-team.ru/arc_vcs/market/jlibrary/market-proto/protobuf-handlers),
они также теперь лежат в аркадии

