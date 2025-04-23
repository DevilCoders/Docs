# skypper
**Sc**ala **y**db wra**pper**. Простая обертка над YDB Java SDK - библиотекой для работы с Yandex Database.

    import ru.yandex.vertis.ydb.skypper.YdbWrapper

    private val commonPool = ExecutionContext.fromExecutor(ForkJoinPool.commonPool())

    val settings = PoolSettings(minSize = 10,
                                maxSize = 50,
                                keepAliveTime = 5.minutes,
                                maxIdleTime = 1.minute,
                                queryCacheSize = 1000)

    val ydb = YdbWrapper(endpoint, database, ydbToken, settings)(commonPool)

Как подключить в проект:

    <dependency>
        <groupId>ru.yandex.vertis.ydb</groupId>
        <artifactId>skypper_2.12</artifactId>
        <version>1</version>
    </dependency>

При обновлении с версии 36 и старше нужно руководствоваться памяткой в файле `migration-37.md`.

Для выпуска новой версии необходимо запустить [действие CI](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fskypper&id=increment-version).

Внутри содержится пул сессий (аналог коннектов в mysql). Сессии создаются по мере надобности, пока их количество не
достигнет maxSize, и остаются в пуле. При выполнении запроса сессия достается из пула и становится недоступна для
других запросов. После выполнения запроса у сессии автоматически вызывается release(), и она
возвращается в пул. Сессии, которые не потребовались ни разу в течение maxIdleTime, удаляются из пула. Каждые
keepAliveTime для всех сессий делается специальный запрос keepAlive, чтобы ydb не забыл про них.

Если количество активных сессий достигло maxSize, последующие запросы встают в очереди. Размер очереди определяется
настройкой waitQueueMaxSize и по умолчанию равно maxSize * 2. Если эта очередь заполнится, последующие запросы за
сессий начнут отваливаться с ошибкой java.lang.IllegalStateException: too many outstanding acquire operations.

Подробнее про саму Yandex Database можно почитать и посмотреть тут:

- https://ydb.yandex-team.ru/docs/
- https://www.youtube.com/watch?v=7u4R5r_vE4U
- https://wiki.yandex-team.ru/Users/darl/Doklady/.files/ydb.pdf

Есть метод stats, который возвращает статистику пула сессий:

    ydb.stats
    // SessionPoolStats{minSize=10, maxSize=50, idleCount=1, disconnectedCount=0, acquiredCount=25, pendingAcquireCount=0}

Можно предзагружать сразу много сессий, чтобы сервис не тупил на старте:

    ydb.preloadSessions(25, timeout = 1.second)

Сессии запрашиваются параллельно пачками по 10 штук. Таймаут ожидания - на создание каждой сессии, настраивается.

В примерах ниже происходит работа с такими табличками:

    CREATE TABLE series
    (
        series_id Uint64,
        release_date Uint64,
        series_info Utf8,
        title Utf8,
        PRIMARY KEY (series_id)
    );

    CREATE TABLE test2
    (
        series_id Uint64,
        idx Uint64,
        title Utf8,
        PRIMARY KEY (series_id)
    );

Которые наполнены такими данными:

    series:
    | series_id | release_date |             series_info |      title |
    |   Some[1] |      Empty[] | Some["Serial Number 1"] | Some["t1"] |

    test2:
    | series_id |     idx |      title |
    |   Some[1] | Some[2] | Some["t1"] |

Библиотека позволяет делать запросы на чтение (с уровнем Online Read-Only или Stale Read-Only), синхронные:

    implicit val titleReads = YdbReads(_.getColumn(0).getUtf8)

    ydb.query("series_title")("select title from series", settings = QuerySettings(readMode = Online))
    ydb.query("series_title")("select title from series", settings = QuerySettings(requestTimeout = 300.millis))

И асинхронные:

    ydb.queryAsync("series_title")("select title from series").onComplete {
      case Success(it) => println(s"got titles: ${it.mkString(", ")}")
    }

stale read-only - уровень, при котором могут возвращаться немного неактуальные данные. online read-only - возвращаются
сравнительно актуальные данные.

В запросах требуется передавать имплицитный экземпляр YdbReads[A], конвертирующий из ResultSet в нужное значение. В
ответе возвращается итератор значений A. Есть дефолтный конвертер YdbReads.Default, которые вернет маппинг
столбцы-значения для каждой строки:

    implicit val titleReads = YdbReads.Default
    val rs = ydb.query("series_title")("select title from series")
    println(rs.getColumn("title"))

Также в запросах требуется указывать "имя запроса" - какой-нибудь краткий строковый идентификатор, который можно писать
в лог или выводить на метрики.

Еще в запросах требуется trace. Можно указывать Traced.empty. Тогда он не будет вписан в запрос.

еще в запросах присутствует неявный параметр RequestContext. С помощью него можно логировать и выводить в метрики
статистику выполнения запросов и транзакций: сколько было ретраев, в какие момент времени, с какими статусами.

Запросы на апдейт (с уровнем serializable read-write), также синхронные и асинхронные:

    ydb.update("series_by_id")("update series set title = 'tt2' where series_id = 1")
    ydb.updateAsync("series_by_id")("update series set title = 'tt2' where series_id = 1")

Они ничего не возвращают. Если статус не Success, вернется исключение, или будет ретрай (в зависимости от кода ошибки).

Для специальных случаев есть метод rawExecute, который дает доступ напрямую к Session из Java SDK. Можно дергать любые
методы самостоятельно и отслеживать их коды возврата. Например, чтобы накатить ddl. Как раз для этого он используется
в skypper в тестах: накатить таблички в базу в докер-контейнере (см. TestDockerConfigBuilder):

     schemaFile.foreach(sql => {
       ydb.rawExecute("ddl") { session =>
         session.executeSchemeQuery(sql).join()
       }
     })

Еще библиотека умеет в транзакции (аналогично, sync и async). Синхронные транзакции могут быть вложенными:

    // читает и обновляет title в таблицах series и test2: t<число> -> t<число+1>
    implicit val reads: YdbReads[String] = YdbReads(_.getColumn(0).getUtf8)

    ydb.transaction("inc_series_title") { executor =>
      val value = executor.query("series_title")("select title from series where series_id = 1").next()
      val next = "t" + (value.replace("t", "").toInt + 1)
      executor.update("series_title")(ydb"update series set title = $next")

      ydb.transaction("inc_test2_title") { executor =>
        val value = executor.query("test2_title")("select title from test2 where series_id = 1").next()
        val next = "t" + (value.replace("t", "").toInt + 1)
        executor.update("test2_title")(ydb"update test2 set title = '$next' where series_id = 1")
      }
    }

Вложенная транзакция не начинает новую, а использует ту, что начата выше (и не пытается коммитить). Таким образом можно
наслаивать логику через stackable traits в единой транзакции (например, разнести апдейты нескольких таблиц по трейтам в
едином методе в одной транзакции). Правда, надо помнить, что YDB не позволяет читать в транзакции данные, которые ранее
были в ней же изменены - будет исключение.

Любое исключение в запросе внутри транзакции, даже если вы обернете его в try-catch, откатывает транзакцию. В случае,
если исключение все же будет обернуто, наружу будет выброшен RollbackException, у которого в cause будет лежать
исходное исключение.

Также RollbackException будет выброшен при любом следующем запросе в транзакции после выставления флага rollbackOnly.

Транзакции работают так: все чтения, сделанные в ходе транзакции, запоминаются. В момент, когда мы делаем commit,
YDB проверяет, что данные остались такие же. Если это не так, commit возвращает ошибку ABORTED: transaction locks
invalidated. И транзакцию надо повторить.

Но YDB действует даже более агресcивно: транзакция, которая заведомо будет инвалидирована - недолгий жилец. Любой
очередной запрос в такой транзакции, не только commit, вернет ABORTED. Все последующие будут возвращать NOT_FOUND:
transaction <id> not found - сервер ее уже удалил.

Такое все надо ретраить. Библиотека любезно все ретраит сама.

Также надо помнить, что нельзя читать данные (строки таблиц), которые ранее были обновлены в этой же транзакции (апдейт
этих строк). Поэтому сначала все читаем, а потом обновляем. Но, например, читать другую таблицу после обновления данной
можно.

Все ошибки, которые можно ретраить, ретраятся:
ABORTED, NOT_FOUND, UNAVAILABLE, TRANSPORT_UNAVAILABLE, OVERLOADED, CLIENT_RESOURCE_EXHAUSTED, BAD_SESSION.

Ошибки OVERLOADED и CLIENT_RESOURCE_EXHAUSTED ретраятся с таймаутом. Таймаут и количество ретраев
можно настраивать. Также можно настраивать таймаут выполнения запросов, создания сессий итд.

На заметку: транзакции, которые делают только апдейт, без чтения - не могут быть инвалидированы.

Асинхронная транзакция могла бы выглядеть так:

    implicit val reads: YdbReads[String] = YdbReads(_.getColumn(0).getUtf8)

    ydb.transactionAsync("inc_series_title") { executor =>
      val resultF = executor.queryAsync("series_title")("select title from series where series_id = 1")
      val result2F = executor.queryAsync("test2_title")("select title from test2 where series_id = 1")
      // и еще, например, много разных чтений параллельно
      for {
        value <- resultF.map(_.next())
        value2 <- result2F.map(_.next())
        next = "t" + (value.replace("t", "").toInt + 1) // логика на клиенте
        // в конце апдейт
        _ <- executor.updateFragmentAsync("series_title")(ydb"update series set title = $next where series_id = 1")
      } yield ()
    }

Но не может. Потому что в сессии нельзя запускать параллельные запросы. Будет ошибка SESSION_BUSY. Точнее, могла бы
быть.

Дело в том, что запрос с данным txId не может выполняться в другой сессии. То есть, транзакция всегда прибита к
сессии, где она начата, а запросы в сессии, как сказано выше, должны выполняться последовательно. Таким образом,
получается, что все запросы в транзакции, не важно, асинхронные или нет, могут выполняться только по одному в каждый
момент времени.

Библиотека поддерживает этот контракт явно, и при попытке начать новый запрос, если уже какой-то выполняется, будет
ошибка RequestInProgressException. Она выставит флаг rollbackOnly (если он еще не выставлен).

Асинхронный вариант будет такой:

    implicit val reads: YdbReads[String] = YdbReads(_.getColumn(0).getUtf8)

    ydb.transactionAsync("inc_series_title") { executor =>
      for {
        value <- executor.queryAsync("series_title")("select title from series where series_id = 1").map(_.next)
        value2 <- executor.queryAsync("test2_title")("select title from test2 where series_id = 1").map(_.next)
        next = "t" + (value.replace("t", "").toInt + 1) // логика на клиенте
        // в конце апдейт
        _ <- executor.updateFragmentAsync("series_title")(ydb"update series set title = $next where series_id = 1")
      } yield ()
    }

Транзакции можно начинать явным session.beginTransaction и коммитить/откатывать в конце явными commit/rollback. Но это
лишние два запроса. YDB api имеет поддержку tx-флагов, передаваемых с запросами, через которые можно сообщить, что данными
запросом мы начинаем транзакцию, а вот этим мы ее коммитим.

Для rollback'а tx-флага нет, надо дергать апи в SessionImpl.

Skypper поддерживает работу с транзакциями через tx-флаги с целью оптимизации. Транзакцию начинает первый запрос в ней.
В настройках запроса можно передать параметр isLast:

    val settings = QueryExecutorSettings(isLast = true)
    executor.update("series_title")(ydb"update series set title = $next where series_id = 1", settings)

Такой запрос закоммитит транзакцию. Если после этого продолжать выполнять запросы, будет ошибка AlreadyCommittedException.

Можно отправлять запросы без указания isLast. Тогда транзакция будет в конце закоммичена явно вызовом commit.

Вместо передачи флага isLast через настройки, можно использовать вызов следующего вида:

    executor.update("series_title").last(ydb"update series set title = $next where series_id = 1")

Такой синтаксис поддерживается для методов `update`, `updateAsync`, `query` и `queryAsync`.

Если в ходе выполнения возникает исключение, библиотека изо всех постарается откатить транзакцию. Важно так или иначе
завершить ее, потому что незакрытые транзакции могут висеть довольно долго. Опыты показывают, что сессия умирает (ошибка
BAD_SESSION) примерно через 10 минут неактивности. Но если в сессии идет какая-то деятельность, даже не связанная с
данной траназкцией, она все равно продолжает висеть.

Библиотека содержит строковый интерполятор ydb"...", позволяющий писать такие запросы
в строку:

    import ru.yandex.vertis.ydb.skypper.syntax._

    implicit val titleReads = YdbReads(_.getColumn(0).getUtf8)

    def getTitle(series_id: Int): Option[String] = {
      ydb.query("title_by_series_id")(
        ydb"select title from series where series_id = $series_id"
      ).take(1).toList.headOption
    }

Запрос ydb"select title from series where series_id = $series_id" будет преобразован в:

    DECLARE $a AS Int32;
    select title from series where series_id = $a

Аргумент series_id будет вынесен в Params. Выносить так можно только то, что стоит в позициях параметров.
Имя таблицы как `String`, например, так указывать не стоит - интерполятор сгенерирует запрос, но в YDB он не пройдет. Вместо этого можно использовать `Fragment.verbatim` и интеполяцию фрагментов:

    import ru.yandex.vertis.ydb.skypper.fragment.Fragment

    val tableName = "some_table"
    val tableFragment = Fragment.verbatim(tableName)
    ydb"select * from $tableFragment"

В примере выше `Fragment.verbatim` создаёт фрагмент без параметров. При интерполяции фрагмента содержащийся в нём SQL-код и его список параметров встраивается в результирующий фрагмент.

Интерполятор поддерживает SQL-контейнеры `List`, `Dict`, `Optional` и `Tuple`. Так, запрос

    val seriesIds = Seq(1, 2, 3)
    ydb"select title from series where series_id in $seriesIds"

будет преобразован следующим образом:

    DECLARE $a AS List<Int32>;
    select title from series where series_id in $a

Поддерживается произвольная вложенность контейнеров. Например, запрос

    val seriesIds = Seq((1,1), (2,1), (3,1))
    ydb"select title from series where (series_id, index_id) in $seriesIds"

будет преобразован:

    DECLARE $a AS List<Tuple<Int32, Int32>>;
    select title from series where (series_id, index_id) in $a

Стоит заметить что YDB не поддерживает передачу списка `VALUES` одним параметром (например, `VALUES $a`) - в SQL-коде должен быть именно список кортежей (`VALUES ($x, $y), ...`). Для этого случая предлагается использовать вспомогательный метод `Fragment.values`.

К примеру,

         val values = (1 to 5).map { idx =>
           (idx, Some(1), "test")
         }
         val valuesFragment = Fragment.values(values)

         ydb"upsert into table (a,b,c) $valuesFragment"

Превратится в

        DECLARE $a AS Int32;
        DECLARE $b AS Int32;
        DECLARE $c AS Utf8;
        DECLARE $d AS Int32;
        DECLARE $e AS Int32;
        DECLARE $f AS Utf8;
        DECLARE $g AS Int32;
        DECLARE $h AS Int32;
        DECLARE $i AS Utf8;
        DECLARE $j AS Int32;
        DECLARE $k AS Int32;
        DECLARE $l AS Utf8;
        DECLARE $m AS Int32;
        DECLARE $n AS Int32;
        DECLARE $o AS Utf8;
        upsert into table (a,b,c) values ($a,$b,$c),($d,$e,$f),($g,$h,$i),($j,$k,$l),($m,$n,$o)

Для случаев где нужно явно указать SQL-тип интерполируемого значения (например, `Uint32` вместо `Int32`), можно использовать следующий синтаксис:

    import ru.yandex.vertis.ydb.skypper.syntax._
    import ru.yandex.vertis.ydb.skypper.fragment.Put.uint32

    ydb"select ${1 as uint32}"

Это превратится в

    DECLARE $a AS Uint32;
    select $a

Если набора поддерживаемых "из коробки" типов недостаточно, можно определить дополнительные инстансы тайпкласса `Put.Typed` - см. примеры в коде `Put`.

Многие запросы сохраняются в кеше. YDB не требуется строить для них AST, поэтому они выполняются немножко
быстрее. В кеш отправляются запросы у которых набор параметров не пустой, либо в настройках которых передан параметр
forceKeepInQueryCache = true.

Skypper использует настройки для полного соответствия стандарту ANSI SQL (https://clubs.at.yandex-team.ru/yql/3166)

Добавляем следующие настройки:

Поведение оконных функций RANK/DENSE_RANK для NULL ключей
В соответствии со стандратом функции  RANK/DENSE_RANK должны трактовать  NULL ключи как равные друг другу и всегда возвращать  Uint64

    PRAGMA AnsiRankForNullableKeys;

Использование COALESCE для ключей JOIN
В соответствии со стандартом в конструкциях вида
SELECT a.* FROM T1 AS a JOIN T2 as b USING(key)
COALESCE ключей  JOIN должен использоваться при наличии  * и совпадении имен ключевых колонок слева и справа.

    PRAGMA DisableCoalesceJoinKeysOnQualifiedAll;

Семантика совместного использования IN и NULL

    pragma AnsiInForEmptyOrNullableItemsCollections;

Порядок выполнения ORDER BY/LIMIT вместе с UNION ALL
По стандарту ORDER BY/LIMIT должен выполняться после UNION ALL

    pragma AnsiOrderByLimitInUnionAll;


Есть поддержка механизма ReadTable для потокового чтения таблиц

Реализованны два метода

    def readTableBatched[A: YdbReads](
                                         name: String
                                       )(tableName: String,
                                         settings: ReadTableBaseSettings = ReadTableBaseSettings(),
                                       )(implicit trace: Traced,
                                         ctx: RequestContext = new RequestContext): Iterator[Seq[(A, TupleValue)]]

    def readTable[A: YdbReads](
                                          name: String
                                        )(tableName: String,
                                          settings: ReadTableBaseSettings = ReadTableBaseSettings(),
                                        )(implicit trace: Traced,
                                          ctx: RequestContext = new RequestContext): Iterator[(A, TupleValue)]

Разница между методами в том, что Batched-метод сразу отдает полученные данные, представляя из себя Iterator.grouped(size),
а не-Batched метод представляет из себя просто Iterator, скрывая подргрузку данных по необходимости внутри себя.

Для использования необходимо передать в фунцкию наименование запроса (name), название таблицы (tableName) и параметры запроса (ReadTableBaseSettings).
Рекоммендуется настраивать ReadTableBaseSettings исходя из ожидаемых данных, а именно выбирать только необходимые стоблцы таблицы (поле columns), и не ставить большой batchSize без необходимости, тк это количество записей будет храниться в памяти.
Так же есть возможность продолжить чтение с определенного элемента(не включая сам элемент), заполнив поле fromKeyExclusive в ReadTableBaseSettings.

Детали реализации:
В момент первого запроса у таблицы запрашивается ее схема, из нее берется первичный ключ таблицы, из которого будет формироваться TupleValue, для возможности продолжить чтение с определенной записи.
Затем по необходимости данные запрашиваются из таблицы порциями (batchSize в ReadTableBaseSettings) и либо сразу возвращаются клиенту, либо сохраняются в паяти, предоставляя интерфейс для чтения.
