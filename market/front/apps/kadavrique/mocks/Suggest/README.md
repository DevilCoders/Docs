# Suggest

Обработка запросов в suggest с клиента. Очень простой.
Добавляете в стейт объект созданный через хелперы:
createSuggestionsMarket(id: string, data: Array), где id - это текстовый запрос пользователя, а data - это ожидаемый ответ сервера.
и аналогичные - createSuggestionsMarketEndingsBlue, createSuggestionsMarketEndings

Хелперы такие, потому что ответы сервера саджеста могут быть очень разными и покачто не хочется делать слишком сложный конструктор этих ответов.

Добавлена обработка ручек:
/suggest-market/suggest-market
/suggest-market/suggest-market-endings
/suggest-market/suggest-market-endings-blue
