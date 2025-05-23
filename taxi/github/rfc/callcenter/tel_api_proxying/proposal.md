## Работа с учетными записями в телефонии

[Постановка задачи в трекере](https://st.yandex-team.ru/TAXIBACKEND-22436)

### Выбор микросервиса

Делаем все в сервисе integration-api-auth, мотивация - там уже есть CRUD по операторам, тесно связано. Возможно его надо переименовать в callcenter_operators?

Выносить проксирование в отдельный сервис пока кажется лишним усложненем: 1. слишком мало логики для отдельного сервиса и 2. проксирование тесно связано с БД операторов


### Аутентификация в АПИ телефонии
- Заводим ключ API для нашего сервиса, TTL 5 лет
- помещаем в секреты
- переиспользуем механизм Жени Кацевмана по авторизации в КЦ

Оценка: `1.5д`

### Общие моменты
- все наши новые ручки работают по `yandex_uuid` оператора из админки
- все 4хх и 5хх ответы от ручек телефонии добавляем в мониторинг
- все ручки, которые проксируют телефонию, сделал через `POST` потому что нет уверенности что их можно кешировать через `GET` и что они ничего не изменяют
- самые большие риски - нет описания многих ручек, не интегрировались раньше с этой системой, они достаточно "внешние" для нас что можно затруднить общение.

### Требования
> При создании учётки оператора нужно заводить его в базе КЦ
- `3д` Новая ручка `POST callcenter_operators/v1/admin/operator/add_to_telephony`
  - идем в ручку телефонии по созданию оператора (ручка не описана! отв. Александр Носков)
  - если оператор успешно заводится в телефонии - ставим флажок что он заведен
  - если получаем `4хх` - отдаем код ошибки вызывающему клиенту
  - в дальнейшем эту ручку надо вызывать отдельно после `POST /v1/operators/add_bulk/`. То есть перекладываем проблемы с транзакционностью на администратора этого списка (кажется что в этом случае так можно)
  - мониторим кол-во успешных/неуспешных походов в АПИ телефонии
- `2д` Новая ручка `POST callcenter_operators/v1/admin/operator/remove_from_telephony`
  - идем в ручку телефонии по удалению/деактивации оператора (ручка не описана! отв. Александр Носков)
  - если ОК то снимаем флажок про заведение в телефонии
  - если получаем `4хх` - отдаем код ошибки вызывающему клиенту
- `1д` доработка ручки `/v1/admin/operators/delete_bulk/`
  - запрещаем удалять тех операторов, которые заведены в телефонии
- `0.5д` добавляем в `GET v1/admin/operators/` флажок "заведен ли в телефонии" для отображения на фронте
- `0.5д` скрипт чтобы прогнать всех текущих операторов через ручку добавления в телефонию (если вручную не получится)

>  при входе оператора в интерфейс нужно запрашивать у КЦ пароль и отдавать его фронту (чтобы оператору не нужно было вводить пароль от телефонии)

- `2д` Новая ручка `POST callcenter_operators/v1/operator/show_password`
  - фактически проксирует ручку телефонии `/USER/xxx/SHOWPASSWORD&REQUEST={'REASON':''} `

>  оператор из интерфейса будет выполнять выход/выход/паузу на линии (редактировать статус только для себя)
- `2д` Новая ручка `POST callcenter_operators/v1/operator/status`
  - чтобы можно было понять текущий актуальный статус для вывода на UI по всем очередям
  - идет в ручку телефонии `mod.cipt-call-center/api/callcenter/AGENT/_CC_ID_/_AGENTID_/SHOW/`
- `1д` Новая ручка `GET callcenter_operators/v1/operator/connection` для получения статуса подключения. Возвращает true, если подключена хотя бы одна очередь
- `1д` Новая ручка `POST callcenter_operators/v1/operator/connection` для вывода на линию и ухода с нее
  - идет в ручку телефонии `mod.cipt-call-center/api/callcenter/AGENT/_CC_ID_/_AGENTID_/CONNECT/_QUEUESNAME_` либо в `mod.cipt-call-center/api/callcenter/AGENT/_CC_ID_/_AGENTID_/DISCONNECT/_QUEUESNAME_`
  - указываем очереди вручную из БД (Носков не советует использовать звездочку из документации, можно уточнить почему)
  
- `1д` Новая ручка `GET callcenter_operators/v1/operator/pause` - на паузе ли оператор. Возвращает true если хотя бы под одной очереди оператор на паузе.
- `1д` Новая ручка `POST callcenter_operators/v1/operator/pause`
  - идет в ручку телефонии `mod.cipt-call-center/api/callcenter/AGENT/_CC_ID_/_AGENTID_/changestatus/_QUEUESNAME_/_priority_/_paused_` и устанавливает паузу и/или приоритет для очередей

>  руководитель операторов будет через админку распределять операторов по линиям (редактировать статусы всех операторов)

Ответ Носкова: "очереди мы на данном этапе вручную заводим, позже будут ручки, привязать оператора к очереди можно в интерфейсе QM, позже будет ручка, я думаю пара месяцев"

Но для того, чтобы можно было передавать вместо звездочки в выходе на линию конкретные очереди - делаем ручку. В будуеще она будет ходить в ручку телефонии, пока - просто записывает в БД.

- `1д` Новая ручка `POST callcenter_operators/v1/operator/set_queues`
  - записывает в нашей БД очереди оператора (нужно для выхода на линию)

## Общее
- `2д` мониторинги
- `0.5д` доработка схемы хранения данных (новые поля) + скрипт миграции + сама миграция
- `3д` тестирование + багфикс
- `0.5д` выкатка + присмотреть за ней
