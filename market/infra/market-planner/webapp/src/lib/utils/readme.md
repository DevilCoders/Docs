# Lodash, moment и прочие зависимости

Хорошая альтернатива Lodash или ambar (пока тот импортирует Lodash) — ((https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/market-planner/webapp/src/lib/utils/fp.ts?rev=7517229 fp хелперы)).

Любая работа над датами часто дублируется, поэтому импорт самого moment должен быть только в ((https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/market-planner/webapp/src/lib/utils/dateTimeUtils.ts?rev=7517229 dateTimeUtils)). А вообще, you dont need moment.

В том случае, если хочется принести в приложение новую зависимость, стоит обратить внимание на ее размер через ((https://bundlephobia.com/ bundlephobia)), а также рассмотреть альтернативы. Например, для создания уникальных идентификаторов может быть достаточным генерация айдишника штатными средствами в 20 строк, без полифица crypto.
