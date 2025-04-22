## Библиотека с базовой функциональностью

1. ```ru.yandex.market.adv.generator.IdGenerator``` - интерфейс для возврата идентификаторов для сущностей.
2. ```ru.yandex.market.adv.service.time.TimeService``` - класс для получения актуального времени.
3. ```ru.yandex.market.adv.loader.file.FileLoader``` - класс для загрузки ресурсов из classpath.
4. ```ru.yandex.market.adv.controller.advice.AbstractResponseEntityExceptionHandler``` - класс, от которого нужно
   наследовать все обработчики исключений в сервисе.
5. ```ru.yandex.market.adv.http.interceptor.TraceInterceptor``` - перехватчик, который добавляет трассировки в запросы
   через okhttp3.
6. ```ru.yandex.market.adv.http.interceptor.MonitoringInterceptor``` - перехватчик, который отправляет в solomon
   мониторинг информацию о кодах ответа больше заданного в конструкторе.
7. ```ru.yandex.market.adv.http.interceptor.RetryInterceptor``` - перехватчик, который повторяет запросы, отправленные
   через okhttp3, если сервис временно недоступен.
8. ```ru.yandex.market.adv.http.interceptor.HttpBodyLoggingInterceptor``` - перехватчик, который записывает в лог тело
   запросов и ответов.
9. ```ru.yandex.market.adv.http.interceptor.TvmInterceptor``` - перехватчик, который добавляет к отправленному запросу
   заголовок X-Ya-Service-Ticket - TVM токен.
10. ```ru.yandex.market.adv.http.properties.HttpClientProperties``` - базовые настройки для http-клиента.
11. ```ru.yandex.market.adv.http.builder.RetrofitBuilder``` - построитель для создания retrofit клиента.
12. ```ru.yandex.market.adv.filter.CommonsJsonRequestLoggingFilter``` - класс-наследник
    от ```CommonsRequestLoggingFilter``` для логирования тела только **application/json** запросов.
