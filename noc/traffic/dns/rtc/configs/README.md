## Обновление конфигов
### Коммит
- коммит происходит стандартно через `svn ci` или через `arc commit`
- тестов нет, поэтому смысла ждать прекомитный проверок никаких, что бы их избежать надо в комментарий добавить `SKIP_CHECK`

### Сборка
Собрать можно несколькими способами:
- **обычный путь** 
   1. зайти в [пайплайн](https://a.yandex-team.ru/projects/dostavkatraffika/ci/releases/timeline?dir=noc%2Ftraffic%2Fdns%2Fci%2Fconfigs_and_scripts&id=release-cs-to-rtc) и нажать кнопку `Run release`
   2. этот пайплайн так же поддерживает сброс yp кеша, который можно включить на вкладке `Custom parameters` перед стартом пайплайна
- **emergency способ 1** - когда мы не хотим коммитить в аркадию или она не работает
   1. если изменения закомичены и sandbox работает, то зайти в [sandbox таску](https://sandbox.yandex-team.ru/task/1355489490/view) в правом верхнем углу нажать кнопку `Clone` и ничего не меняя кнопку `Run`, ждём пока таска примет статус `SUCCESS`
   2. идём в каждый няня сервис на вкладку `Instance Spec`, нам нужно в самом конце `List of layers to assemble instance FS` и нужно отредактировать ресурс `DNS_TT_RTC_CONFIGS_BUNDLE` в поле `Task Id` вписываем номер таски из пункта 1, поле `Resource Id` станет пустым, выбираем из выпадающего списка ресурс содержащий у себя в название `DNS_TT_RTC_CONFIGS_BUNDLE`, нажимаем сохранить
   3. сохраняем ещё раз, но уже всю новую спеку и активируем полученный снапшот. Пункт 2-3 повторить на каждом сервисе. 
- **emergency способ 2** - когда мы не хотим коммитить в аркадию/она не работает и sandbox работает медленно
   1. в [каталоге с нашими конфигами](https://a.yandex-team.ru/svn/trunk/arcadia/noc/traffic/dns/rtc/configs?preview=true), в консоле говорим `ya package bundle.json`, должны получить под ногами tar.gz по типу `yandex-traffic-dns-configs-rtc-bundle.$rev_num.tar.gz` 
   2. говорим команду `ya upload -T DNS_TT_RTC_CONFIGS_BUNDLE --ttl 360 yandex-traffic-dns-configs-rtc-bundle.$rev_num.tar.gz` в ответ получим `Resource link` который открываем и запоминаем `Task ID` который написан в табе справо или на вкладке `Dependent tasks` 
   3. идём в каждый няня сервис на вкладку `Instance Spec`, нам нужно в самом конце `List of layers to assemble instance FS` и нужно отредактировать ресурс `DNS_TT_RTC_CONFIGS_BUNDLE` в поле `Task Id` вписываем номер таски из пункта 2, поле `Resource Id` станет пустым, выбираем из выпадающего списка ресурс содержащий у себя в название `DNS_TT_RTC_CONFIGS_BUNDLE`, нажимаем сохранить
   4. сохраняем ещё раз, но уже всю новую спеку и активируем полученный снапшот. Пункт 3-4 повторить на каждом сервисе
