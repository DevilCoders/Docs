hprof-intermediary
=====

### Что это такое
  Это инструментарий для отображения и скачивания hprof-дампов java-приложений. На серверах приложений должен быть установлен `hprof-courier` (исправляется добавлением своей группы в воркфлоу `hprof-courier`). Демон собирает информацию по hprof-дампам и складывает ее в `zookeper`. Морда есть своя для тестинга и прода соответственно.

#### Как это работает
Заходим на морду, видим список-зебру, выбираем нужный - жмем тычку с кругляшком - `API` делает `OPTIONS` запрос до курьера: таким образом проверяется доступность курьера и его подпроцесса, отвечающего за выдачу файла по http. После успешной проверки курьер дергается уже GET запросом, а вы выбираете место, куда сохранить вывалившийся дамп.

#### Что-то сломалось
Создать таску в очереди `VSADMIN` с компонентом `Vertis-Duty`, в задаче описать с какого хоста и, какой, собственно, дамп не получается скачать (наверное это надо писать в вики, а не здесь, ну да ладно)

##### TODO:
  * Сделать фильтрацию записей по полям: `host`, `project`, `date`
  * Сделать сортировку по возрасту, группировку по хостам и названиям проектов
