## yhttp::client
Класс с базовой функциональностью HTTP клиента.

### Интерфейс
```C++
struct client
{
  response run(task_context_ptr ctx, request req);
  response run(task_context_ptr ctx, request req, const options& options);
  void async_run(task_context_ptr ctx, request req, callback_type callback);
  void async_run(task_context_ptr ctx, request req, const options& options, callback_type callback);
};
```

### Возможности
- последовательный перебор ip4 и ip6 адресов при подключении (в порядке приоритета)
- HTTP Keep-Alive
- multipart запросы
- chunked-ответы
- TSKV логи
- отправляет таймаут в миллисекундах в заголовке X-Request-Timeout
- защита от перегрузок
