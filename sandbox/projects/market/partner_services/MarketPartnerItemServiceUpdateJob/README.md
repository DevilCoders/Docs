Данная задача копирует данные из таблицы YT и взаимодействует с сервисом Market Access по HTTPS через TVM-авторизацию. 

# Подготовка
Для её работы в любом случае потребуется получить `YT_TOKEN` – токен Yandex Table

Далее всё зависит от ситуации

Для отладки потребуется получить `TVM_TICKET` (действителен в течение часа с момента получения, необходимо переодически обновлять вручную)

Для prod необходимо получить:
- `SELF_TVM_ID` – TVM-id сервиса, от имени которого производится запрос (клиента)
- `DST_TVM_ID` – TVM-id сервиса, к которому производится запрос
- `SELF_TVM_SECRET` – секретная строчка TVM сервиса
## Как получить YT_TOKEN
1. Заходим на страницу [oauth.yt.yandex.net](https://oauth.yt.yandex.net/ "Внешняя ссылка (откроется в новом окне)")
2. Жмём Give me my token и даем разрешение.

[Источник](https://wiki.yandex-team.ru/market/analytics/stackoverflow-analitiki-marketa/yt/gde-vzjat-token-dlja-yt/)

## Как получить SELF_TVM_ID и DST_TVM_ID
1. Заходим на [ABC](https://abc.yandex-team.ru/)
2. Через поиск находим нужные сервисы
3. Открываем у каждого вкладку `Ресурсы` и находим блок `Паспорт (TVM приложение)`
4. Внутри блока находим ресурс, в нём нужно поле `ID`
5. Если в этом блоке отсутствуют ресурсы, обратитесь к TVM менеджеру этого сервиса с просьбой создать необходимый ресурс

## Как получить SELF_TVM_SECRET
Получить его можно из того же ресурса, где был взят `SELF_TVM_ID`.
Необходимо из ресурса перейти в Секретницу, где будет единственный ключ, которые необходимо скопировать.

**Учитывайте, что доступ к секрету есть только у TVM менеджера или руководителя сервиса**

## Как получить TVM_TICKET
Предварительно необходимо иметь следующие вводные:
- Получены `SELF_TVM_ID` и `DST_TVM_ID`
- На компьютере, с которого будет получен тикет, существует ssh rsa ключ, который добавлен в staff
- На компьютере установлена `ya` (можно посмотреть [тут](https://docs.yandex-team.ru/devtools/intro/quick-start-guide) в разделе **Установка ya**)
1. Выполняем команду `ya tool tvmknife`
2. Далее вызываем `tvmknife get_service_ticket sshkey --src $SRC -- dst $DST`, где SRC и DST – TVM-id сервисов, клиента и сервера соответственно (учитываете расположение исполняемого файла, он должен отобразиться после установки)
3. В выводе команды будет отображаться тикет
[Источник](https://wiki.yandex-team.ru/passport/tvm2/debug/#kakavtomatizirovatpoxodvchuzhoeapi)

# Настройка
На данный момент для предоставления всех вышеперечисленных параметров задаче используется секретница.

Соответственно, необходимо создать новый секрет и добавить все вышеуказанные параметры (использовать те же имена, но все буквы маленькие)

На данный момент в коде жёстко прописан id секрета (переменная `secret_id` в файле `__init__.py`). Его необходимо заменить на тот, что будет использоваться.

Для того, чтобы впоследствии sandbox мог с ним работать, необходимо предоставить доступ к этому секрету (смотреть [тут](https://docs.yandex-team.ru/sandbox/dev/secret) раздел **Способ 2. Обратиться к секрету во время выполнения задачи.**)