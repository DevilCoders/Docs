# Накопилось много кампаний

## Подходящие ситуации

- в API / степах / веб-интерфейсе при добавлении новой кампании возвращается ошибка:
   - _Превышено максимальное количество незаархивированных кампаний_
   - _Превышено максимальное количество кампаний_
   - _Достигнуто максимальное количество кампаний_
- кампании не удаляются через интерфейс

## Решение
Проставить кампаниям этого клиента `statusEmpty="Yes"` в БД.  
Пример решения с клиентом at-direct-dna-smart-tester.

Сначала нужно узнать номер шарда, выполните запрос на ppcdev 
```sh
dbs-sql *нужная база (test/devtest/dev7)*:ppc:all -q "select * from users where ClientID=*Ваш ClientID*"
```
Запрос пробегается по всем шардам и тот с которого прилетит ответ и есть нужный вам.
Гарантируется что все данные отдельно взятого клиента лежат на одном шарде

Открой интерактивный клиент к нужной базе (ТС/девтест/дев7 и шарду):
```sh
dbs-sql ts:ppc:20
```
Посмотри, что там за кампании:
```sql
select type, count(*) from campaigns where uid = 919073098 and statusEmpty = 'No' group by type;
```
Вывод (запиши его и запрос куда-нибудь, например в тикет, он может пригодиться) :
```text
+-------------+----------+
| type        | count(*) |
+-------------+----------+
| wallet      |        1 |
| performance |      999 |
+-------------+----------+
2 rows in set (0.01 sec)
```
Затем выстави кампаниям признак "удалена":
```sql
update campaigns set statusEmpty = 'Yes' where uid = 919073098 and statusEmpty = 'No' and type in ('performance');
Query OK, 999 rows affected (0.06 sec)
Rows matched: 999  Changed: 999  Warnings: 0
```
Проверь результат:
```sql
select type, count(*) from campaigns where uid = 919073098 and statusEmpty = 'No' group by type;
```
```text
+--------+----------+
| type   | count(*) |
+--------+----------+
| wallet |        1 |
+--------+----------+
1 row in set (0.00 sec)
```

{% note alert %}

Осторожнее с этим способом: не удалите кошелек (кампанию с типом **wallet**) или все кампании под ним (оставьте хотя бы одну).

{% endnote %}

### Нужно чтобы кампании действительно удалилась? {#prepare-for-delete}
Описанный выше способ "заметает кампанию под ковёр".
Если повезет — её подберет и удалит скрипт `ppcClearEmptyCampaigns.pl`, но скорее всего он не сможет удалить кампанию, а вместе с ней объявления и другие объекты.

Нужно сделать так, чтобы кампании удовлетворили условиям проверок "пригодности к удалению".
Помогут в этом вот эти запросы к базе (подставь нужный ClientID в каждый):
```sql
DELETE q.* FROM bs_export_queue q JOIN campaigns c USING(cid) WHERE ClientID = 6865906;
DELETE q.* FROM bs_export_candidates q JOIN campaigns c USING(cid) WHERE ClientID = 6865906;
UPDATE campaigns SET sum = 0, sum_spent = 0, sum_last = 0, sum_to_pay = 0, shows = 0, clicks = 0, OrderID = 0, statusActive = 'No', statusBsSynced = 'No', statusModerate = 'No', archived = 'No', currencyConverted = 'No' WHERE statusEmpty = 'Yes' AND ClientID = 6865906;

```
Скрипт `ppcClearEmptyCampaigns.pl` по факту удаляет кампанию через N дней.
Можно ускорить процесс удаления добавив запись в очередь `camp_operations_queue` и другой скрипт `ppcCampQueue.pl` удалит кампанию целиком в течении нескольких минут (в зависимости от объема очереди в этом шарде):
```sql
# запросы выше надо выполнить до добавления задания в очередь, чтобы кампания удовлетворяла условиям на удаление
INSERT INTO camp_operations_queue (cid, operation) SELECT cid, "del" FROM campaigns WHERE ClientID = 6865906 and statusEmpty="Yes";
```

## Ссылки
- [DIRECT-164395: При удалении кампании в steps-api добавлять кампанию в очередь camp_operations_queue](https://st.yandex-team.ru/DIRECT-164395)
- [DIRECT-129463: Ошибки в тестах "Steps API: Can not call method with name: saveNewCampaign and args"](https://st.yandex-team.ru/DIRECT-129463)
- [DIRECT-105486: ТС: cлишком много кампаний у at-transport-tester-7](https://st.yandex-team.ru/DIRECT-105486)
- [DIRECT-105535: Разобраться с избытком кампаний у тестовых пользователей](https://st.yandex-team.ru/DIRECT-105535)
- [DIRECT-134375: UserObjectsCountTest падает с Проверка не пройдена](https://st.yandex-team.ru/DIRECT-134375)
