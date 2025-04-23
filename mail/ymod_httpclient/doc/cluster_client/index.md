## yhttp::cluster_client
Надстройка над yhttp::client с дополнительными возможностями по улучшению отказоустойчивости.

### Интерфейс
```C++
struct cluster_client
{
  void async_run(task_context_ptr ctx, request req, callback_type callback);
  void async_run(task_context_ptr ctx, request req, const options& options, callback_type callback);

  // Адаптер для синхронного вызова и корутин
  template <typename CompletionToken>
  auto async_run(task_context_ptr ctx, request req, const options& options, CompletionToken&& token);
};
```

### Возможности
- все возможности yhttp::client
- ретраи в один хост или по списку
- бюджет ретраев (не больше % ретраев в общей массе запросов)
- прогрессивные ретраи (backoff+jitter)
- умеет останавливать ретраи по заголовку X-Request-NoRetry в ответе сервера
- отправляет номер попытки (с нуля) в заголовке X-Request-Attempt
- балансировка запросов по списку хостов с динамическим вычислением весов в зависимости от ответов
