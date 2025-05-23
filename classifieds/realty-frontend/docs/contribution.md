# Процесс работы над задачей

1. Каждое изменение должно сопровождаться отдельной задачей в трекере. Задача должна быть создана исключительно в
очереди `REALTYFRONT`, если задача изначально сформулирована кем-то в иной очереди,
она должна быть **перенесена** (не продублирована) в очередь [`REALTYFRONT`](https://st.yandex-team.ru/REALTYFRONT/). При переносе сохраняется история, комментарии и список наблюдателей.
1. Под каждое изменение заводится отдельная фича-ветка, ответвленная от текущей релизной ветки (`trunk`).
1. Разработчик пишет код.
1. По окончании разработки, разработчик создается пулл-реквест (драфт),
указывая в описании что было сделано, на что обратить внимание и какие проекты затронуло.
1. После создания пулл-реквеста автоматически запускаются тесты и поднимаются демо-стенды с измененными проектами (не все проекты умеют поднимать такие стенды)
1. Если тесты пройдены, то разработчик паблишит пул-реквест, автоматически назначаются ревьюеры (при необходимости можно руками добавить кого-то), тикет автоматически переводится в `В ревью/In Review`.
    * Ревью маленьких задач может выполнять один разработчик.
    * Для больших задач – два и более ревьюеров. Желательно создавать перед ревью встречу с рассказом о том, что было сделано и на что обратить внимание.
1. Происходит ревью кода, при необходимости он отдается на доработку, а задача в треке переоткрывается ревьюером.
Разработчик вносит правки отдельным коммитом. **Не нужно сквошить правки** по пулл-реквесту с остальным кодом.
1. После того как ревьювер одобрит `PR`, разработчик [собирает демо-стенд](./deploy.md), если он не был собран автоматически.
1. Если задача не требует ручного тестирования (см. раздел ниже), то разработчик переводит задачу в трекере в статус `Без тестирования/Without testing`, иначе в статус `Можно тестировать/Ready For Test`. Так же нужно убедиться, что ветка базируется на актуальном транке и нет конфликтов.
1. В случае если есть конфликты или нужно обновиться на транк следует использовать rebase, а не merge (так как rebase позволяет оставить историю чистой).
1. Если во время тестирования были обнаружены баги, то тестировщик переоткрывает задачу.
Разработчик снова вносит правки отдельным коммитом, **без сквоша**. При необходимости опять запускает процесс ревью
1. Когда тестирование пройдено, тестировщик ставит статус в трекере `Протестировано/Tested` и назначает релизную дату.
Работа над тикетом закончена

## Рекомендации по TBD-разработке

После переезда в Аркадию стараемся переходить с Git Flow разработки задач на Trunk Based Development. Рекомендации по TBD разработке оформлены в [отдельном документе](./tbd.md).

## Задачи без ручного тестирования
Есть несколько случаев, когда задачу можно перевести в статус не требующего тестирования от команды QA:
- Тривиальные изменения с точечными правками в коде, которые может проверить сам разработчик и ревьюер. Пример: поправил текст в переводах, поправил файл конфигураций, добавил правило в CSP, правка в robots.txt, перезаливка статики, поменять иконку, прокинуть дополнительный параметр в ручку.
- Небольшие вёрсточные задачи, которые правят внешний вид компонентов, при условии, что на компонент написаны скриншотные тесты. Если скриншотных тестов на компонент нет, то хорошей практикой является добавить такие тесты. Пример: переделал верстку баннера, изменил внешний вид блока ссылок.
- Небольшие изменения логики работы модулей кода, при условии, что на них написаны unit-тесты, проверяющие старые и новые кейсы. Пример: поправил модуль форматирующий телефон.
- Инфраструктурные задачи, которые протестировать лучше разработчика не сможет больше никто и не требующие регресса. Пример: добавил дополнительные логи, добавил счетчик клиентских ошибок.

Если возникают сомнения вокруг того, можно ли отдать задачу в статус "без тестирования", то сначала стоит понять, почему у вас возникли такие сомнения. Если вы за что-то опасаетесь, не уверены в корректности работы вашего изменения, то значит, вероятно, нужно прояснить волнующие моменты и убедиться, что вы сделали то, что требуется в задаче. Не стоит перекладывать ответственность на команду QA, помните, что за ваш код ответственны вы сами, а труд ручного тестирования повышается в цене в условиях высокого спроса, используйте его с умом! Если вы всё равно сомневаетесь со статусом, то спросите команду QA.

## Именование веток

Имя фича-ветки должно **полностью совпадать** с идентификатором задачи в трекере из очереди `REALTYFRONT`.

## Текст сообщения коммита

Текст сообщения итогового коммита, попадающего в релизную ветку, должен соответствовать шаблону:
```
[task_name]
[desc]
```
 * `task_name` - название задачи в трекере
 * `desc` - более подробное описание (не обязательно).

 Если изменения ОЧЕНЬ минорные и не хочется мешать их с задачами, эти изменения можно залить в `trunk` без тестирования с названием `TRIVIAL: описание`.

## Чек-лист разработчика

1. **До того как писать код:**
    1. Нужно точно понять формулировку тикета, если что-то непонятно, лучше уточнить у ответственного продукта о том, что он хочет
    1. Определить место проекта, в которое будет вноситься изменение
    1. **Подумать, зачем делается тикет и как он будет влиять на текущий бизнес-процесс**
    1. Найти самому по коду или спросить другие места, которые, возможно, будут задеты тикетом у коллег/тестирования. Например,
       добавляем новое поле в форму создания/редактирования оффера в личном кабинете, в этом случае мы неявно задеваем фиды, карточку оффера, фильтры в таче/десктопе

1. **Во время написания кода:**
    1. Обращать внимание на ошибки в консоли и в логах ноды
    1. Смотреть, как сделан похожий функционал в других частях проекта

1. **Перед отдачей в ревью:**
    1. Перечитать тикет. Проверить, все ли в итоге сделано по описанию в нем
    1. Просмотреть дифф в PR самостоятельно на предмет ошибок/лишнего (саморевью)
    1. Проверить все переснятые скриншоты глазами, все ли там ок
    1. Добавить описание в PR. Прокомментироавть в PR спорные моменты, на что стоит обратить особое внимание при ревью
    1. Проверить, что все чеки прошли
    1. Проверить, что стенд собрался и на нем нужная версия /version
    1. Потыкать стенд, проверить еще раз, что всё работает

1. **Перед отдачей в тестирование:**
    1. Добавить в тикет изменения, которые проговаривались лично или в чатиках и не отражены
    1. Если в ПР затронут функционал, который напрямую не описан в тикете - добавить описание этих моментов для тестирования, что еще им нужно проверить
    1. Проверить актуальность ребейза на транк
    1. Потыкать стенд, проверить еще раз, что всё работает
