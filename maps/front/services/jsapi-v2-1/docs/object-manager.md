Зачем и как сделаны модули можно почитать в [публичной документации](https://tech.yandex.ru/maps/doc/jsapi/2.1/dg/concepts/object-manager/about-docpage/)

Ниже в общих чертах описано внутреннее устройство:

  * `DataLoadController` — сущность, которая решает, когда и какие данные нужно запросить с сервера.
  * `ObjectContoller` | `GridClusterer` — сущности, получающие на вход некоторый набор данных и карту. Решают, какие объекты нужно сейчас отрисовать на карте, а какие нужно скрыть. В случае использования `GridClusterer` на основе входных данных могут быть сформированы кластеры.

![RemoteObjectManager](images/object-manager-remote.png)

![LoadingObjectManager](images/object-manager-loading.png)

![ObjectManager](images/object-manager.png)
