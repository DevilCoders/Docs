# Подключение к БД с рабочих машин

## PostgreSQL { #postgres }

Для подключения к PG используется т.н. connection URL, имя пользователя и пароль. Для дева и тестинга логин и пароль общие на всю команду, для прода каждый заходит под своим staff-логином и секретным паролем. Доступ в продовую БД только на чтение за исключением дежурных и техлида.

Окружение | Логин | Секрет с паролем
:---|:---|:---
Локально/дев|market_mbo_mdm_unstable|[тут](https://yav.yandex-team.ru/secret/sec-01esg686dppkbcepwa92fqrjtq/explore/versions)
Тестинг|market_mbo_mdm_testing|[вот тут](https://yav.yandex-team.ru/secret/sec-01es18y2xkbkd9tea5t1znysp4/explore/versions)
Продакшен|Ваш staff-логин|поиск по логину [здесь](https://yav.yandex-team.ru)

Connect URL для окружений:
- Локально/дев: `jdbc:postgresql://sas-xarucvrr29dxqu86.db.yandex.net:6432,vla-gyatmh1xpyf2ce8w.db.yandex.net:6432/market_mbo_mdm_unstable?sslmode=require&targetServerType=master&prepareThreshold=0`
- Тестинг: `jdbc:postgresql://sas-29mp30z4fdu2xbvs.db.yandex.net:6432,vla-s6o2etdyu0ve8xhb.db.yandex.net:6432/market_mbo_mdm_testing?sslmode=require&targetServerType=master&prepareThreshold=0`
- Прод: `jdbc:postgresql://vla-dqt67khwduoqsarz.db.yandex.net:6432,sas-0e4mewc2xzs0icjr.db.yandex.net:6432/market_mbo_mdm_production?sslmode=require&targetServerType=master&connectTimeout=15&loginTimeout=30`

{% note info "Пароли" %}

Если в секрете больше одного пароля, следует брать тот, который `sql.newPassword`.

{% endnote %}

{% note warning %}

Все пароли кроме дева являются секретными. Ни в коем случае не вставляйте их `Ya Paste`, телеграм, тикеты или почту. Если вам нужно поделиться паролем, то скиньте ссылку на соответствующий секрет в [Vault](https://yav.yandex-team.ru). МДМ находится под надзором внешних аудиторов - все ходы записаны.

{% endnote %}

**Подключение в IDEA**
1. На панели Database создайте новое подключение с драйвером PostgreSQL. Если не можете найти панель, два раза нажмите Shift и введите `Database`.
2. Выберите тип подключения URL Only.
3. Введите Connect URL, имя пользователя и пароль
   ![Пример заполнения](../../_images/db_connect_1.png "Пример заполнения")
4. На вкладке SSH/SSL поставьте галочку Use SSL и укажите путь к CA File. Если у вас его нет, то скачать его можно [здесь](https://crls.yandex.net/allCAs.pem) и сделать ему `chmod 0600`.
   ![Пример заполнения](../../_images/db_connect_2.png "Пример заполнения")
5. На вкладке Schemas выберите все схемы, содержащие в названии `mdm`.

{% note tip "Для Mac OS" %}

Если не взлетело, то в настройках подключения попробуйте в VM Options прописать `-Djava.net.preferIPv4Stack=false`.

{% endnote %}

## Yt

В Yt мы фактически не используем write-подключения, т.к. процедура записи в Yt не такая тривиальная, как в SQL-базах. А для чтения чаще используется [YQL](https://yql.yandex-team.ru/). Почти все ключевые таблицы лежат в подпапках корневого пути `//home/market/ваше_окружение/mdm`, например, [здесь](https://yt.yandex-team.ru/markov/navigation?path=//home/market/production/mdm) (мета) или [здесь](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/mdm) (одна из реплик).
