maps::ydb
===================
Helper library which makes simple YDB operations easier. The goal of this library is to help you to write less code for the simple cases. For the complex transactions you can use TTableClient directly.
The library helps with following:
  * Throws `YdbError` on unsuccessful response status
  * Less code to specify request parameters
  * Less code for simple transactions
  * Helps to parse query results
  * Supports [maps::introspection](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/introspection) for simple parsing of the results.

[Official YDB С++ client](https://a.yandex-team.ru/arc/trunk/arcadia/kikimr/public/sdk/cpp) is very powerful and flexible, but it requires to write a lot of code for the simple cases. See [the official examples](https://a.yandex-team.ru/arc/trunk/arcadia/kikimr/public/sdk/cpp/examples/basic_example/basic_example.cpp?rev=5275594#L527).

## Usage example
Assuming that you have prerequisites for YDB [basic_example](https://ydb.yandex-team.ru/docs/getting_started/start_cpp/).
You could declare an introspectable structure with static method `columns`:
```c++
    struct Episode {
        uint64_t seriesId;
        uint64_t seasonId;
        uint64_t episodeId;
        uint64_t air_date;
        std::string title;
        
        static auto columns()
        {
            return std::make_tuple(
                "seriesId", "seasonId", "episodeId", "air_date", "title"
            );
        }

        template<typename T>
        static auto introspect(T& episode)
        {
            return std::tie(
                episode.seriesId,
                episode.seasonId,
                episode.episodeId,
                episode.air_date,
                episode.title
            );
        }
    };
```
Then for prepared parametrized queries you could simply write:
```c++
    maps::ydb::YdbClient db("ydb-ru.yandex.net:2135", "/ru/home/yourlogin/mydb");
    db.upsert(
        Episode{2, 1, 1, 16166, "Minimum Viable Product"}
    );
    db.upsert(
        Episode{2, 1, 2, 16173, "The Cap Table"}
    );

    std::vector<Episode> episodes = db.select<Episode>(
        R"(
            DECLARE $seriesId AS Uint64;
            DECLARE $seasonId AS Uint64;
            DECLARE $episodeId AS Uint64;

            SELECT air_date, title
            FROM episodes
            WHERE series_id = $seriesId AND season_id = $seasonId AND episode_id = $episodeId;
        )",
        "$seriesId", seriesId,
        "$seasonId", seasonId,
        "$episodeId", episodeId
    );
    Cout << episodes.at(0).title;
```

The same example with official YDB library will look like this:
```c++
    //! Shows usage of prepared queries.
    static TStatus PreparedSelectTransaction(TSession session, const TString& path,
        ui64 seriesId, ui64 seasonId, ui64 episodeId, TMaybe<TResultSet>& resultSet)
    {
        // Once prepared, query data is stored in the session and identified by QueryId.
        // Local query cache is used to keep track of queries, prepared in current session.
        TString query = R"(
            DECLARE $seriesId AS Uint64;
            DECLARE $seasonId AS Uint64;
            DECLARE $episodeId AS Uint64;

            SELECT air_date, title
            FROM episodes
            WHERE series_id = $seriesId AND season_id = $seasonId AND episode_id = $episodeId;
        )");

        // Prepare query or get result from query cache
        auto prepareResult = session.PrepareDataQuery(query).GetValueSync();
        if (!prepareResult.IsSuccess()) {
            return prepareResult;
        }

        auto dataQuery = prepareResult.GetQuery();
        auto params = dataQuery.GetParamsBuilder()
            .AddParam("$seriesId")
                .Uint64(seriesId)
                .Build()
            .AddParam("$seasonId")
                .Uint64(seasonId)
                .Build()
            .AddParam("$episodeId")
                .Uint64(episodeId)
                .Build()
            .Build();

        auto result = dataQuery.Execute(TTxControl::BeginTx(TTxSettings::SerializableRW()).CommitTx(),
            params).GetValueSync();

        if (result.IsSuccess()) {
            resultSet = result.GetResultSet(0);
        }

        return result;
    }

    void PreparedSelect(TTableClient client, const TString& path, ui32 seriesId, ui32 seasonId, ui32 episodeId) {
        TMaybe<TResultSet> resultSet;
        ThrowOnError(client.RetryOperationSync([path, seriesId, seasonId, episodeId, &resultSet](TSession session) {
            return PreparedSelectTransaction(session, path, seriesId, seasonId, episodeId, resultSet);
        }));

        TResultSetParser parser(*resultSet);
        if (parser.TryNextRow()) {
            auto airDate = TInstant::Days(*parser.ColumnParser("air_date").GetOptionalUint64());

            Cout << airDate.FormatLocalTime("%a %b %d, %Y") << " "
                 << *parser.ColumnParser("title").GetOptionalString()
                 << Endl;
        }
    }


    TString endpoint = "ydb-ru.yandex.net:2135";
    TString database = "/ru/home/yourlogin/mydb";
    TString path = database;

    auto driverConfig = TDriverConfig()
        .SetEndpoint(endpoint)
        .SetDatabase(database)
        .SetAuthToken(GetEnv("YDB_TOKEN"));

    TDriver driver(driverConfig);
    TTableClient client(driver);
    PreparedSelect(client, path, 2, 3, 7);
```

## Interface
### YdbClient
YdbClient is a wrapper class for YDB driver and TTableClient. You create YdbClient once in your service to connect to the database:
```c++
    maps::ydb::YdbClient db(
        <endpoint>,
        <database path>,
        <OAuth token>
    );
```
Note: in case of incorrect database settings, the library will throw exception on the first database request, not on the YdbClient construction.
How to get YDB endpoint: https://ydb.yandex-team.ru/docs/getting_started/setup_network_access/
About OAuth token: https://ydb.yandex-team.ru/docs/getting_started/start_auth/

### Introspectable structures
The library provides simple interface for operations with introspectable structures from [maps::introspection](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/introspection) library.
The structure should provide:
  * `introspect` method with non-const access to the fields;
  * `columns` method which provide the names for the database columns in the same order as the fields in `introspect` method.

Example of the `Entity` structure:
```c++
    struct Entity {
        std::string id;
        int32_t value;
        
        static auto columns()
        {
            return std::make_tuple("id", "value");
        }

        template<typename T>
        static auto introspect(T& entity)
        {
            return std::tie(entity.key, entity.value);
        }
    };
```

### Basic operations
YdbClient provides following high-level operations:
  * `upsert(<table name>, <introspectable object>)` - inserts or updates a single record to the table. See [YQL tutorial](https://yql.yandex-team.ru/Tutorial/ydb_11_Upsert_into) for the operation details.
```c++
    db.upsert("entities", Entity{"some id", 32});
```

  * `select<Entity>(<query>, <args...>)` - performs a select query and returns the result as the vector of the introspectable structures.
Query should return a single result set. Multiple results (like `SELECT * FROM A; SELECT * FROM B;`) in single query are not supported.
Request parameters should be [declares](https://yql.yandex.net/docs/ydb/syntax/declare/) in the YQL query. The request parameters could be passed to the `select` method as a key-value pairs or as an introspectable structure.
```c++
    std::vector<entities> result0 = db.select<Entity>(
        "SELECT * FROM entities"
    );

    TString query1 = R("
        DECLARE $id AS String;
        SELECT * FROM entities
        WHERE id == $id;
    )";
    std::vector<entities> result1 = db.select<Entity>(
        query1, "$id", "some id"
    );

    TString query2 = R("
        DECLARE $id AS String;
        DECLARE $value AS Int32;
        SELECT * FROM entities
        WHERE id < $id AND value < $value;
    )";
    std::vector<entities> result2 = db.select<Entity>(
        query2, Entity{"some id", 32}
    );
```
`select` method also supports tuple to represent the output. Do not use tuple with `SELECT *`, since it will depend on the order of columns in the result.
```c++
    auto values = db.select<std::tuple<int32_t>>("SELECT value FROM entities");
```

  * `selectOne<Entity>(<query>, <args...>)` - same as select, but returns the first result. Throws `maps::ydb::EmptyError` for an empty query result. This method is useful for queries with some calculation:
```c++
    const auto& [sumVal, maxVal] = db.selectOne<std::tuple<uint64_t, uint64_t>>(
        "SELECT SUM(value) as sum, MAX(value) as max FROM entities"
    );
```

  * `runQuery(<query>, <args...>)` - performs the YQL query and returns `TVector<NYdb::TResultSet>`.This method helps with parameters formatting, but does not help you with the results parsing.
Request parameters should be [declares](https://yql.yandex.net/docs/ydb/syntax/declare/) in the YQL query. The request parameters could be passed to the `runQuery` method as a key-value pairs or as an introspectable structure.
`runQuery` method is useful for the queries which does not have returns values. Like `DELETE`:
```c++
    db.runQuery(
        R"(
            DECLARE $id AS String;
            DELETE FROM entities WHERE id = $id;
        )",
        "$id", "some id"
    );
```

The methods above have following properties for the YDB queries:
  * The query will run synchronously. YdbClient uses `client.RetryOperationSync` and `GetValueSync` inside.
  * The query will be [prepared](https://ydb.yandex-team.ru/docs/getting_started/start_cpp/#_7). We assume that you will use the query more than once in your service. YdbClient uses session.PrepareDataQuery inside.
  * The query will be [parametrized](https://ydb.yandex-team.ru/docs/getting_started/start_cpp/#_6). Less chance that someone will try to include the parameters into the query - less chance of YQL-injection.
  * The query will be executed with [SerializableRW isolation](https://ydb.yandex-team.ru/docs/concepts/transactions/). YdbClient uses `TTxControl::BeginTx(TTxSettings::SerializableRW()).CommitTx()` inside.

### Exceptions
Official YDB library requires you to check `TStatus` for success. YdbClient methods will throw `maps::ydb::YdbError` (derived from `maps::RuntimeError`) with error message inside. Also you can use `maps::ydb::throwOnError(const NYdb::TStatus& status)`, if you work with `TTableClient` directly.
See: https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/ydb/include/errors.h

### Supported types
maps::ydb library uses C++ types to deduce YDB types for the request parameters formatting and parsing.
The library supports only following subset of [the available YDB types](https://ydb.yandex-team.ru/docs/concepts/datatypes/):
 * `String` - `std::string` for result parsing and `std::string_view` for parameters formatting.
 * `Datetime` - `TInstant`, represents time moment up to seconds.
 * `Double` - `double`
 * `Uint32` - `uint32_t`
 * `Int32` - `int32_t`
 * `Uint64` - `uint64_t`
 * `Int64` - `int32_t`

Complex YDB types (like List or Dict) currently are NOT supported.

### Tests with local YDB
YDB provides [ya.make recipe](https://a.yandex-team.ru/arc/trunk/arcadia/kikimr/public/tools/ydb_recipe/README.md) to bring up local YDB instance for unit tests.
See test_helpers.h for helper function `maps::ydb::getLocalYdb()` to connect to the local YDB database in the unit tests.
Provide an empty OAuth token for the local YDB.

### Low-level interface
If you need some more complex transactions or have some complicated case for result parsing, you still can use low-level helper functions from maps::ydb library:
  * `runQuery` - returns `TVector<NYdb::TResultSet>`. So you can use `runQuery` to format request parameters and have direct access to the [NYdb::TResultSet for the results parsing](https://ydb.yandex-team.ru/docs/getting_started/start_cpp/#_4).
  * `client` - provides an access to underlying `TTableClient`. You could use direct access to `TTableClient` for [complex transactions with intermediate data processing in C++ code](https://ydb.yandex-team.ru/docs/getting_started/start_cpp/#_8).
  * `throwOnError` from `errors.h` - checks `TStatus` and throws `YdbError` with error message inside in case or error.
  * `buildParams` from [params.h](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/ydb/include/params.h) - helps to fill `TParamsBuilder` with request parameters.
  * `parse<Entity>` and `parseValue` from [parse.h](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/ydb/include/parse.h) - help to extract the result from the `TResultSetParser`.

See corresponding header files for more details.
