# Таблицы DynamoDB

В [бессерверном режиме работы](serverless-and-dedicated.md#serverless) базы данных {{ ydb-name }} вы можете использовать _документные таблицы_.

Документные таблицы {{ ydb-name }} совместимы с [таблицами Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.CoreComponents.html#HowItWorks.CoreComponents.TablesItemsAttributes).

Документная таблица содержит данные в виде набора элементов. При создании документной таблицы обязательно требуется задать первичный ключ, который служит уникальным идентификатором элементов таблицы.

Элемент – это группа атрибутов. Каждый элемент имеет уникальный идентификатор или первичный ключ, который отличает его от всех остальных в таблице. Первичный ключ представляет собой набор атрибутов. Все элементы таблицы обязаны содержать атрибуты, входящие в первичный ключ таблицы. За исключением первичного ключа, элементы могут содержать произвольные атрибуты произвольных типов. Элементы документных таблиц во многом похожи на строки, записи или кортежи в других СУБД.

Атрибут — единица данных, представленная в документной таблице в виде пары ключ-значение, атрибуты во многом похожи на поля или столбцы в других СУБД.

Для работы с документными таблицами [используйте Document API](../docapi/tools/aws-setup.md). Работа через [YDB API]{% if lang == "en" %}((https://ydb.tech/en/docs/reference/ydb-sdk/){% endif %}{% if lang == "ru" %}(https://ydb.tech/ru/docs/reference/ydb-sdk/){% endif %} возможна только в режиме чтения.
