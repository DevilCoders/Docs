# UDFка для отладочной печати значений атрибутов

На вход принимает название атрибута из [списка](https://a.yandex-team.ru/arc/trunk/arcadia/robot/library/oxygen/indexer/output/attr_printer/attr_printer.cpp?rev=3938718#L774) и значение атрибута в виде строки.

Пример:
    PRAGMA udf("debug_lib.so");

    $nullvalue = cast(null as string);

    SELECT
        Debug::PrintAttribute('Ui8Array', '0ab23') as a
        , Debug::PrintAttribute('timestamp', '1534533453') as b
        , Debug::PrintAttribute('blah', $nullvalue) as c
    --    , Debug::PrintAttribute('blah', 'aaa') as d --terminates
    ;
