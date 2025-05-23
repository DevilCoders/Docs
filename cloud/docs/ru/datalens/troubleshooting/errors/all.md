# Все ошибки

На странице приведены коды ошибок и их описание.
Чтобы посмотреть подробную информацию об ошибке, перейдите по ссылке, нажав на код ошибки:

Код ошибки | Описание |
----- | ----- |
[ERR.CHARTS.REQUEST_SIZE_LIMIT_EXCEEDED](ERR-CHARTS-REQUEST_SIZE_LIMIT_EXCEEDED.md) | Request size limit exceeded |
[ERR.CK.TOO_MANY_LINES](ERR-CK_TOO_MANY_LINES.md) | Too many series on the chart |
[ERR.DS_API.CONNECTION_CONFIG.SUBSELECT_NOT_ALLOWED](ERR-DS_API-CONNECTION_CONFIG-SUBSELECT_NOT_ALLOWED.md) | Subquery source is disallowed in the connection settings |
[ERR.DS_API.DATABASE_UNAVAILABLE](ERR-DS_API-DATABASE_UNAVAILABLE.md) | Data source is unavailable |
[ERR.DS_API.DB.AUTHENTICATION_FAILED](ERR-DS_API-DB-AUTHENTICATION_FAILED.md) | Database authentication failed |
[ERR.DS_API.DB.CANNOT_PARSE.DATETIME](ERR-DS_API-DB-CANNOT_PARSE-DATETIME.md) | Cannot parse datetime |
[ERR.DS_API.DB.CANNOT_PARSE.NUMBER](ERR-DS_API-DB-CANNOT_PARSE-NUMBER.md) | Cannot parse number |
{% if audience == "internal" %}[ERR.DS_API.DB.CHYT.AUTH_FAILED](ERR-DS_API-DB-CHYT-AUTH_FAILED.md) | Authentication failed |{% endif %}
{% if audience == "internal" %}[ERR.DS_API.DB.CHYT.CLIQUE.ACCESS_DENIED](ERR-DS_API-DB-CHYT-CLIQUE-ACCESS_DENIED.md) | Access to clique <название клики> for user <логин пользователя> was denied |{% endif %}
{% if audience == "internal" %}[ERR.DS_API.DB.CHYT.CLIQUE.INVALID_SPECIFICATION](ERR-DS_API-DB-CHYT-CLIQUE-INVALID_SPECIFICATION.md) | Invalid clique specification. Probably, clique does not exists |{% endif %}
{% if audience == "internal" %}[ERR.DS_API.DB.CHYT.CLIQUE.NOT_RUNNING](ERR-DS_API-DB-CHYT-CLIQUE-NOT_RUNNING.md) | Clique <название клики> is not running |{% endif %}
{% if audience == "internal" %}[ERR.DS_API.DB.CHYT.CLIQUE.SUSPENDED](ERR-DS_API-DB-CHYT-CLIQUE-SUSPENDED.md) | Clique <название клики> is suspended |{% endif %}
{% if audience == "internal" %}[ERR.DS_API.DB.CHYT.INVALID_SORTED_JOIN.MORE_THAN_ONE_TABLE](ERR-DS_API-DB-CHYT-INVALID_SORTED_JOIN-MORE_THAN_ONE_TABLE.md) | Cannot join a concatenation of tables with another table |{% endif %}
{% if audience == "internal" %}[ERR.DS_API.DB.CHYT.INVALID_SORTED_JOIN.NOT_A_KEY_COLUMN](ERR-DS_API-DB-CHYT-INVALID_SORTED_JOIN-NOT_A_KEY_COLUMN.md) | Column used in join expression is not a key column |{% endif %}
{% if audience == "internal" %}[ERR.DS_API.DB.CHYT.INVALID_SORTED_JOIN.NOT_KEY_PREFIX_COLUMN](ERR-DS_API-DB-CHYT-INVALID_SORTED_JOIN-NOT_KEY_PREFIX_COLUMN.md) | Joined columns should form prefix of joined table key columns |{% endif %}
{% if audience == "internal" %}[ERR.DS_API.DB.CHYT.SUBQ_WEIGHT_LIMIT_EXCEEDED](ERR-DS_API-DB-CHYT-SUBQ_WEIGHT_LIMIT_EXCEEDED.md) | Subquery exceeds data weight limit |{% endif %}
{% if audience == "internal" %}[ERR.DS_API.DB.CHYT.TABLE_ACCESS_DENIED](ERR-DS_API-DB-CHYT-TABLE_ACCESS_DENIED.md) | Access to table was denied |{% endif %}
{% if audience == "internal" %}[ERR.DS_API.DB.CHYT.TABLE_HAS_NO_SCHEMA](ERR-DS_API-DB-CHYT-TABLE_HAS_NO_SCHEMA.md) | YT table has no schema. Only schematized tables are supported |{% endif %}
[ERR.DS_API.DB.COLUMN_DOES_NOT_EXIST](ERR-DS_API-DB-COLUMN_DOES_NOT_EXIST.md) | Requested database column does not exist |
[ERR.DS_API.DB.JOIN_COLUMN_TYPE_MISMATCH](ERR-DS_API-DB-JOIN_COLUMN_TYPE_MISMATCH.md) | Columns in JOIN have different types |
[ERR.DS_API.DB.MATERIALIZATION_NOT_FINISHED](ERR-DS_API-DB-MATERIALIZATION_NOT_FINISHED.md) | Data is not available because materialization is not yet complete |
[ERR.DS_API.DB.MEMORY_LIMIT_EXCEEDED](ERR-DS_API-DB-MEMORY_LIMIT_EXCEEDED.md) | Memory limit has been exceeded during query execution |
[ERR.DS_API.DB.SOURCE_CONNECT_ERROR](ERR-DS_API-DB-SOURCE_CONNECT_ERROR.md) | Data source refused connection |
[ERR.DS_API.DB.SOURCE_DOES_NOT_EXIST](ERR-DS_API-DB-SOURCE_DOES_NOT_EXIST.md) | Data source (table) does not exist |
[ERR.DS_API.DB.SOURCE_ERROR.TIMEOUT](ERR-DS_API-DB-SOURCE_ERROR-TIMEOUT.md) | Data source timed out |
[ERR.DS_API.DB.ZERO_DIVISION](ERR-DS_API-DB-ZERO_DIVISION.md) | Division by zero |
[ERR.DS_API.FIELD.NOT_FOUND](ERR-DS_API-FIELD-NOT_FOUND.md) | Unknown field |
[ERR.DS_API.FIELD.TITLE.CONFLICT](ERR-DS_API-FIELD-TITLE-CONFLICT.md) | Field title conflicts with another field |
{% if audience == "internal" %}[ERR.DS_API.FILTER.INVALID_VALUE](ERR-DS_API-FILTER-INVALID_VALUE.md) | Filter invalid value |{% endif %}
[ERR.DS_API.FORMULA.UNKNOWN_FIELD_IN_FORMULA](ERR-DS_API-FORMULA-UNKNOWN_FIELD_IN_FORMULA.md) | Unknown field found in formula |
[ERR.DS_API.FORMULA.UNKNOWN_SOURCE_COLUMN](ERR-DS_API-FORMULA-UNKNOWN_SOURCE_COLUMN.md) | Unknown referenced source column |
[ERR.DS_API.FORMULA.VALIDATION.AGG.INCONSISTENT](ERR-DS_API-FORMULA-VALIDATION-AGG-INCONSISTENT.md) | Inconsistent aggregation among operands |
[ERR.DS_API.FORMULA.VALIDATION.LOD.INCOMPATIBLE_DIMENSIONS](ERR-DS_API-FORMULA-VALIDATION-LOD-INCOMPATIBLE_DIMENSIONS.md) | Incompatible dimensions |
[ERR.DS_API.FORMULA.VALIDATION.LOD.INVALID_TOPLEVEL_DIMENSIONS](ERR-DS_API-FORMULA-VALIDATION-LOD-INVALID_TOPLEVEL_DIMENSIONS.md) | Invalid top-level LOD dimension found in expression |
[ERR.DS_API.FORMULA.VALIDATION.WIN_FUNC.BFB_UNSELECTED_DIMENSION](ERR-DS_API-FORMULA-VALIDATION-WIN_FUNC-BFB_UNSELECTED_DIMENSION.md) | Window function has unselected dimension |
[ERR.DS_API.FORMULA.VALIDATION.WIN_FUNC.NO_AGG](ERR-DS_API-FORMULA-VALIDATION-WIN_FUNC-NO_AGG.md) | Window function has no aggregated expressions among its arguments |
[ERR.DS_API.REFERENCED_ENTRY_ACCESS_DENIED](ERR-DS_API-REFERENCED_ENTRY_ACCESS_DENIED.md) | Referenced connection <идентификатор подключения> cannot be loaded: access denied |
[ERR.DS_API.ROW_COUNT_LIMIT](ERR-DS_API-ROW_COUNT_LIMIT.md) | Received too many result data rows |
[ERR.DS_API.SOURCE_ACCESS_DENIED.INVALID_TOKEN](ERR-DS_API-SOURCE_ACCESS_DENIED-INVALID_TOKEN.md) | Invalid user token |
[ERR.DS_API.SOURCE_CONFIG.TABLE_NOT_CONFIGURED](ERR-DS_API-SOURCE_CONFIG-TABLE_NOT_CONFIGURED.md) | Table is not ready yet |
[ERR.DS_API.US.ACCESS_DENIED](ERR-DS_API-US-ACCESS_DENIED.md) | Access denied |
{% if audience == "internal" %}[Нет прав на просмотр данных](no-access-to-read-this-operation.md) | You have no access to read this operation |{% endif %}
