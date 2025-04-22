Пакет, реализующй идею "самоописывающихся" выражений.

Случается, что есть некоторая логика, для которой хочется иметь некоторое визуально представление - схему, словесное описание, в общем, что-то, что можно прочитать/посмотреть и понять, как оно работает, не залезая в код и не разбираясь в нем.

Пакет состоит из следующего:
* интерфейс Expr<I, R>, описывающий абстракцию "выражение, принимающее на вход I и возвращающее результат R"
* наследники-реализации интерфейса Expr (Cases, IfElse, Value, пр.) для описания простейших вычислений
* интерфейс ExprHandler, описывающий абстракцию "как обработать описанное Expr-ом выражение"
* различные реализации ExprHandler:
  * EvaluateExprHandler - вычислять Expr
  * EvaluateNullAndDescribeAllExprHandler - описывать весь Expr, ничего не вычисляя
  * EvaluateAndDescribeEvaluatedExprHandler - вычислять Expr и описывать только то что вычислялось
  * EvaluateAndDescribeAllExprHandler - вычислять Expr, описывать весь Expr с пометками, что вычислялось

Пример использования всего этого (на момент написания единственный :) ) можно посмотреть в [OffersProcessingStatusService](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mbo-category/mboc-common/src/main/java/ru/yandex/market/mboc/common/services/offers/processing/OffersProcessingStatusService.java)

