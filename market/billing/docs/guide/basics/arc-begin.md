# Советы по Аркадии новичкам
**Справка по командам:** [https://docs.yandex-team.ru/arc/ref/commands](https://docs.yandex-team.ru/arc/ref/commands)

**Чат поддержки в Telegram** [https://t.me/joinchat/EPm1hEXREWprMLUdqsQ7Mw](https://t.me/joinchat/EPm1hEXREWprMLUdqsQ7Mw)

**FAQ:** [https://wiki.yandex-team.ru/arcadia/arc/faq/](https://wiki.yandex-team.ru/arcadia/arc/faq/)

## Настройки бинов
Иногда IDEA не может проиндексировать данные, и это частично связано с отсутствием в модулях Spring. Открываете настройки
проекта File -> Project Structure -> Modules. Выбираете интересующий вас модуль, щелкаете правой кнопкой мыши. Add->Spring.
Выделяете все, жмете пробел, следом клавишу ОК. После этого перезапускаете IDEA.

## IDEA не видит классы
Надо перезагрузить кэш индекса: `File -> Invalidate Caches -> Invalidate and Restart`

## Создание веток { #branch }
Всегда переключайтесь в trunk для создания новой ветки, поскольку новая ветка создается на
основе текущей выбранной. Чтобы иметь локально самую свежую версию trunk, не забудьте сделать pull Последовательность команд следующая:
```
arc checkout trunk
arc pull
arc checkout -b NEW_BRANCH_NAME
```
После этого можете работать с версией, которая ничем не будет отличаться от серверной.

### Советы по именованию веток
Для удобства предлагается называть локальные ветки с помощью двух компонент, разделенных `/`

Первая часть:
* feature (создание дополнительной функциональности)
* bugfix (исправление бага)

Вторая часть состоит из названия тикета, для решения которого была создана ветка.

Пример:
`feature/MARKETBILLING-103`

## Сохранение изменений { #save }
Для того, чтобы добавить определенный файл в коммит, требуется выполнить команду
```
arc add FILE_PATH
arc commit -m COMMIT_DESCRIPTION
```
или
```
arc commit -f FILE_PATH -m COMMIT_DESCRIPTION
```
Если вы хотите сохранить изменения во всех файлах, то вместо флага `-f FILE_PATH` можно просто прописать `-a`.

В COMMIT_DESCRIPTION стоит коротко описать, какие изменения привнес коммит в формате
TICKET_NAME: что добавили.

Пример: `MARKETBILLING-67: страничка про дежурство`

Если вы хотите проигнорировать какие-то изменения, то можете выполнить команду `arc stash`

После этого выполняете команду `arc push -u users/YOUR_USER_NAME/LOCAL_BRANCH_NAME` для отправки данных на сервер.

Не забудьте заменить YOUR_USER_NAME на ваше доменное имя, а LOCAL_BRANCH_NAME на название локальной ветки (см. советы по именованию веток)

Если не был создан PR, то создаем.

## Как создать pull request
### IDEA
необходимо нажать кнопку `VCS -> Create Pull Request...`

![картинка где кнопка](_assets/pull-request-creation-from-idea.png)


можно выбрать разные опции PR, потом нажать OK

![картинка интерфейс](_assets/pull-request-creation-from-idea-2.png  )
### terminal
Для этого выполнить `arc pr create -m PULL_REQUEST_DESCRIPTION`


В качестве PULL_REQUEST_DESCRIPTION лучше использовать следующую комбинацию:
TICKET_NAME: TICKET_HEADER.

Пример: `MARKETBILLING-103: Сделать правки в документацию маркет-биллинга`

## Где посмотреть и как опубликовать Pull Request

### Где посмотреть?
После успешного создания PR в терминале появляется ссылка на arcanium.

Если ссылка потерялась, заходим на [arcanium](https://a.yandex-team.ru/) и нажимаем `Outgoing`. Откроется интерфейс со списком несмержденных пулл реквестов.

![картинка меню пулл реквестов](_assets/arcadia-outgoing-button.png)

Далее можно выбрать любой PR из списка и перейти к нему, нажав на id.

### Как опубликовать Pull Request
![картинка интефейс пулл реквеста](_assets/pull-request-interface.png)


**Перед тем как публиковать необходимо проверить несколько вещей**
* Проходят ли все тесты
* Если вы меняли liquibase файлы для __oracle__ и не накатывали изменения, то необходимо запустить [liquibaseDev.sh](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/liquibaseDev.sh), также необходимо запускать [dumpSchema.sh](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/dumpSchema.sh) ([вики на эту тему](https://wiki.yandex-team.ru/users/gaklimov/db-unit/dump-schema/)), чтобы обновить sql файлы для unit-тестов. Обновление unit-test файлов можно посмотреть в дирректори `market/mbi/mbi/mbi-db/src/sql/unittest/MARKET_BILLING/`. Эти файлы необходимы для тестирования и при изменении их необходимо добавлять в коммит.

**Если все в порядке можно нажать Publish**
 
Это действие отправит уведомление для assingees, чтобы они могли сделать code review.

**Еще необходимо поменять статус тикета на Code Review**
![картинка code review статус тикета](_assets/ticket-code-review-button.png)
**А также ометить компоненты, которые были редактированы.** 
![картинка code review статус тикета](_assets/ticket-module-choose.png)

### У меня возник **merge conflict** что делать?
Merge conflict возникает, когда два человека редактируют одни и те же строчки.
Чтобы разрешить конфликт, мы смотрим на наши изменения и изменения другого человека и решаем как код должен выглядеть в итоге. 
Команды которые помогут, появляются на правом крае интерфейса, но их легко написать самому.

```
$arc fetch users/<yandex_login>/<branch_name> # мы скачиваем нашу ветку с сервера
$arc checkout users/<yandex_login>/<branch_name> # переходим на нашу ветку
$arc pull trunk # обновляем локальную копию trunk
$arc rebase trunk # производим rebase, накатываем коммиты из своей ветки поверх свежих изменений из trunk
```

Конфликт можно разрешить через интефейс [IDEA](https://www.jetbrains.com/help/idea/resolving-conflicts.html#distributed-version-control-systems) или [ручками](https://docs.yandex-team.ru/devtools/src/arc/conflict) 

**Если вы поняли что сильно накосячили, то можно откатить rebase**
```
arc reset --hard ORIG_HEAD
```

[**FAQ по вопросам arc**](https://wiki.yandex-team.ru/arcadia/arc/faq/#jasdelalrebaseivseslomal.chtodelat)



## Ревью бот
Также существует бот , который упрощает код ревью и помогает людям, которые не любят читать почту.

[telegram](https://t.me/codereview_bot)

[документация и полезные команды](https://github.yandex-team.ru/devexp/devexp#Поддерживаемые-команды)

## Откат изменений
Если в ходе работы один из коммитов был кривой, то можно выполнить откат до нужного коммита.

Для начала открываете лог аракдии `arc log` и ищете номер последнего нужного вам коммита.

Следом прописываете команду по откату:
```
arc reset --soft COMMIT_NUMBER
```
В данном случае софт не изменяет уже сохраненные файлы, а просто меняет состояние изменений.

Вместо `--soft` можно также использовать флаг `--hard` для принудительной перезаписи файлов,

если коммиты вам не нужны. Следом меняете что хотите, коммитите нужный файл и отправляете его

принудительно на сервер командой `arc push -f`

## Примечание
Порой при перезагрузке рабочего ноутбука может исчезнуть проект в папке  `~/arcadia/`. Это значит, что его надо заново

смонтировать и перезагрузить в систему для применения последних версий. Делается это с помощью следующих команд:
```
arc mount -m arcadia/ -S store/
cd arcadia
ya ide idea --group-modules=tree -r="/Users/YOUR_USER_NAME/work/arc_mbi" --directory-based --yt-store  -l
```
При выполнении данной команды не забудьте заменить `YOUR_USER_NAME` на ваше доменное имя.
