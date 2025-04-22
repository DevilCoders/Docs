# tmv
обёртка над https://a.yandex-team.ru/arc/trunk/arcadia/iceberg/inside-passport-tvm2/
Cделана интеграция с нашими пропертями и некоторые полезные штуки.

TLDR: В коде Директа см. TvmInterceptor и аннотацию @AllowServices

## Как это работает

Основная функциональность представлена интерфейсом  `TvmIntegration`. Есть 2 реализации: обычная и в stub. stub используется в том случае, если tvm интеграция для приложения не нужна(в настройках не задано  `tvm.enabled=true` ) <p>
Обычная реализация прокидывает конфиг в  `inside-passport-tvm2`. Для каждого приложения есть свой `client_id` и секрет. Они настраиваются тут https://abc.yandex-team.ru/services/direct/resources/?supplier=14&type=50&type=47&view=consuming.
Все известные сервисы, нужные директу, должны быть записаны в enum'е `TvmService`<p>
В `app-%.conf` записан `client_id` текущего приложения(на данный момент есть только для intapi) и пусть к файлу секрета. При запуске сервис ходит в tvm-api, получает список публичных ключей, генерирует тикеты, используя серкет и `client_id` с помощью библиотеки https://a.yandex-team.ru/arc/trunk/arcadia/library/ticket_parser2.
Он делает это в отдельном потоке с переодичностью в час. <p>
В `TvmIntegration` 3 метода:<p>
1. `TvmService getTvmService(String ticket) throws IncorrectTvmServiceTicketException;`
получить по тикету название сервиса, владельца тикета.
Используется таким образом: в интерсепторе из реквеста получаем хедер с телом тикета, определяем какой сервис к нам пришел. <p>
2. `String getTicket(TvmService service);`
сгенерировать тикет для сервиса.
Используется таким образом: говорим, в какой сервис хотим пойти, получаем тело тикета и выставляем в хедер при запросе.<p>
3. `TvmService currentTvmService();`
Получить название текущего сервиса. Сервис определеяется в app.conf параметром `tvm.app_id`, который соответствовать одному из значений enum'а `TvmService`.
## Что нужно сделать
Согласно требованиям ИБ секреты нельзя коммитить, поэтому они разложены на ppcdevах и ТС в файлах.
Чтобы локально всё заработало, необходимо записать секрет в `~/.tvm2_direct_intapi` для intapi(путь прописан в intapi app-development.conf), который можно посмотреть на ppcdev: `/etc/direct-tokens/tvm2_direct-test`
