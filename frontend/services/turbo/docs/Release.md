## Релизы

Турбо живёт в СЕРПовом метапакете шаблонов и соответственно в СЕРПовом кластере report-renderer, использует [search priemka](https://wiki.yandex-team.ru/serp/serp-machines/#prijomkarelizov).

## ВАЖНО! ПЕРЕД ОТВЕДЕНИЕМ РЕЛИЗА УБЕДИТЬСЯ В ТОМ, ЧТО НИКТО В ДАННЫЙ МОМЕНТ НЕ СОБИРАЕТ РЕЛИЗ

### Релиз из dev'а
1. [Отвести релизную ветку](https://quigon.yandex.ru/project.html?projectId=Serp_Util_ReleaseTools&tab=projectOverview)
  * выбрать конфигурацию «новый релиз»
  * нажать «отвести» в правом верхнем углу
  * выбрать проект — «turbo»
  * поправить поля «автор, исполнитель, копия»
  * нажать «run build»
2. Дождаться [сборки динамики](
https://sandbox.yandex-team.ru/tasks/?order=-updated&type=SANDBOX_CI_TURBO&page=1&pageCapacity=20&forPage=tasks&desc_re=release). Тикет в sandbox может сфейлиться из-за выросшей статики, например. Убедитесь, что фейл ожидаемый и переходите к следующему пункту
3. Дебиан пакет со статикой собирается и выкаладывается на статический кластер в сабтаске `SANDBOX_CI_TURBO_STATIC_DEBIAN`. Убедитесь, что сборка прошла успешно
4. [Добавить](https://quigon.yandex.ru/viewType.html?buildTypeId=Serp_Turbo_Release_BufferBuild) тэг «RC» нужной сборке (как правило это последняя сборка)
  * проверить, что хэш коммита в описание сборки совпадает с хэшом HEAD коммита в релизной ветке
    ![build commit hash](https://jing.yandex-team.ru/files/zumra6a/2017-08-23_11-33-58.jpg)
5. После этого можно просить [релиз-менеджера](https://staff.yandex-team.ru/sanity) собрать метапакет и выложить его на [приёмку](https://templates.priemka.yandex.ru). ~[Собрать метапакет](https://wiki.yandex-team.ru/users/sanity/howto/#sborkametapaketa) и [выложить его на приёмку](https://wiki.yandex-team.ru/users/sanity/howto/#deplojjmetapaketanabetudljatestirovanija), если вы уверены в своих силах.~ (Лена просит не делать этот пункт самостоятельно, можно сломать процесс другим командам)

Автоматически будет создана задача в очереди `SEAREL`, для удобства нужно проставить задаче тег [turbo-templates](https://st.yandex-team.ru/SEAREL/order:updated:false/filter?tags=turbo-templates).

В случае возникновения проблем — канал `#infraduty` в https://serpyandex.slack.com

#### Добавить задачу в релиз
1. Заходим в конфигурацию [добавить задачу](https://quigon.yandex.ru/viewType.html?buildTypeId=Serp_Util_ReleaseTools_AddIssue) в TeamCity
2. Нажимаем кнопочку «run»
3. Выбираем проект «turbo»
4. В «куда» пишем название релизной ветки
5. Номер задачи опускаем
6. Выбираем номер PR, который нужно влить в веточку
7. Нажимаем «run build»
8. После окончания сборки нужно повторить шаги 2-5 (собрать статику, проставить тэг RC, etc)

#### Релиз
После того, как релизная задача получает статус «Tested», пишем [релиз-менеджеру](https://staff.yandex-team.ru/sanity), что пакет готов к релизу.
