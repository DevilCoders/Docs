# RefreshMon - сервис мониторинга доставки документов в SAMOHOD

## Configuration
Конфигурация логгера хранится в файле `logging.ini`.
Конфигурация приложения хранится в файле `app.ini` в следующем формате:
```ini
[logbroker]
endpoint=vla.logbroker.yandex.net:2135  # Хост:порт логброкера
topics=saas/refresh/prod/topics/shard-0-6552,saas/refresh/prod/topics/shard-13106-19658,saas/refresh/prod/topics/shard-19659-26212,saas/refresh/prod/topics/shard-26213-32765,saas/refresh/prod/topics/shard-32766-39318,saas/refresh/prod/topics/shard-39319-45872,saas/refresh/prod/topics/shard-45873-52425,saas/refresh/prod/topics/shard-52426-58978,saas/refresh/prod/topics/shard-58979-65533,saas/refresh/prod/topics/shard-6553-13105  # Список топиков (через запятую), из которых надо забирать документы для проверки
consumer=saas/refresh/delivery-monitoring/consumers/0  # Путь к консьюмеру, который будет читать топики
tvm_id=%(LOGBROKER__TVM_ID)s  # (см. Environment variables)
tvm_secret=%(LOGBROKER__TVM_SECRET)s  # (см. Environment variables)
dsts_tvm_id=2001059  # TVM ID сервиса, в котором требуется пройти аутентификацию
mercury_out_timestamp_field=Document.ModificationTimestamp  # Название поля в объекте TMessage, содержащего timestamp выхода документа из Mercury
wait_timeout=10  # Время ожидания ответа от логброкера (в секундах)
max_wtime_lag=60  # Время (в секундах) с момента записи документа в логброкер, в течение которого мы считаем документ свежим и не пропускаем
max_mtime_lag=60  # Время (в секундах) начиная с ModificationTimestamp, в течение которого мы считаем документ свежим и не пропускаем

[search]
upper_search_url=https://hamster.yandex.ru/yandsearch  # Endpoint верхнего метапоиска, на который нужно ходить с запросами
int_search_url=http://man1-0471.search.yandex.net:7200/yandsearch  # Endpoint инта, на который нужно ходить с запросами
upper_cgi_params=srcskip=QUICK&rearr=only_samohod_on_middle&rearr=NewsFromQuickUpper_off&json_dump=searchdata.docs  # CGI-параметры для запроса к верхнему метапоиску
int_cgi_params=fsgta=_SearcherHostname&gta=_BaseTimestamp&nocache=da&nofastcache=1&pron=save_l1_factors&ms=proto&hr=json  # CGI-параметры для запроса к инту
base_cgi_params=  # CGI-параметры для запроса к базовому поискую
max_upper_rps=10  # Максимальный RPS к верхнему метапоиску
max_int_rps=30  # Максимальный RPS к инту
max_base_rps=10  # Максимальный RPS к базовому поиску
max_retry_count=5  # Максимальное количество попыток получить информацию о документе из верхнего, среднего или базового поисков (после превышения документ отбрасывается)
index_timeout=3600  # Время (в секундах), по истечению которого документ считается пропавшим (если он не успел появиться на поиске)
allowable_error_sec=1  # Допустимая погрешность (в секундах) в определении времени попадания на поиск (чем больше, тем репрезентативнее выборка; влияет на время, если оно определяется эмпирически)

[golovan]
unistat_host=::  # Хост, на котором запускается unistat-ручка (для IPv6 используется ::, для IPv4 127.0.0.1 или 0.0.0.0)
unistat_port=80  # Порт, на котором запускается unistat-ручка
unistat_path=/stat  # Endpoint unistat-ручки

[golovan.tags]  # Теги для сигналов в Golovan
itype=rtcsmall
ctype=none
prj=saas-refresh-mon-production
```
Если файлы конфигов лежат рядом с бинарником, то используются они. Иначе - используются конфиги по-умолчанию, зашитые в ресурсы бинарника (app.ini и logging.ini из репозитория). Такой хак необходим для прохождения импорт-тестов!

## Environment variables
`LOGBROKER__TVM_ID` - TVM ID для доступа к LogBroker

`LOGBROKER__TVM_SECRET` - TVM Secret для доступа к LogBroker

## Signals
Все сигналы описаны в модуле `utils.messages`. Для добавления нового сигнала его достаточно объявить в модуле `utils.messages` по аналогии с другими сигналами. Unistat-ручка автоматически подтянет новый сигнал после перезапуска.

1. `index_time_dhhh` - Гистограмма времени индексации документа (время появления на поиске минус время выхода из Mercury)
2. `lost_docs_count_summ` - Количество потерянных документов (которые не успели доехать до поиска за время `index_timeout`)
3. `indexed_docs_count_summ` - Количество успешно проиндексированных документов
4. `checked_docs_count_summ` - Количество проверенных документов (должно быть примерно равно max_int_rps * time, но не всегда)
5. `checked_new_docs_count_summ` - Количество новых проверенных документов (которые еще не проверялись до текущего момента)
6. `not_found_docs_by_url_count_summ` - Количество документов, которые перестали искаться по URL на инте после индексации базовым
7. `not_found_docs_by_title_with_quotes_count_summ` - Количество документов, для которых поиск по их title в кавычках (в верхнем метапоиске) вернул пустую выдачу
8. `not_found_docs_by_title_without_quotes_count_summ` - Количество документов, для которых поиск по их title без кавычек (в верхнем метапоиске) вернул пустую выдачу
9. `upper_invalid_response_count_summ` - Количество запросов, на которые верхний метапоиск ответил неизвестной ошибкой
10. `int_invalid_response_count_summ` - Количество запросов, на которые инт ответил неизвестной ошибкой
11. `base_invalid_response_count_summ` - Количество запросов, на которые базовый поиск ответил неизвестной ошибкой
12. `int_answer_is_not_complete_count_summ` - Количество запросов к инту, в ответе которых поле `DebugInfo.AnswerIsComplete == false`
13. `int_error_response_count_summ` - Количество запросов к инту, в ответе которых поле `ErrorInfo.GotError == 1`
14. `rotten_write_time_docs_count_summ` - Количество пропущенных документов из-за давности записи в логброкер (настраивается в параметре max_wtime_lag)
15. `rotten_modify_time_docs_count_summ` - Количество пропущенных документов из-за давности ModificationTimestamp (настраивается в параметре max_mtime_lag)
16. `docs_not_contains_in_result_page_count_summ` - Количество документов, которые после индексации не попали на первую страницу СЕРПа
17. `expected_docs_count_axxx` - Количество документов, в данный момент находящихся в очереди в ожидании появления на поиске (вычисляется эмпирически, поэтому может немного запаздывать)
18. `invalid_modification_timestamp_count_summ` - Количество документов, у которых Document.ModificationTimestamp > now()
19. `timedelta_between_modification_and_current_time_dhhh` - Гистограмма разницы между Document.ModificationTimestamp и now() (значения пушатся только при положительной разнице)
20. `refresh_mon_docs_lifetime_dhhh` - Гистограмма времени жизни документа в сервисе refresh_mon от получения из логброкера до сигнала `index_time_dhhh` или `lost_docs_count_summ`

## TODO
* Ограничить RPS к базовому поиску по хостам (сейчас ограничивается кол-во вызовов функции, делающей запрос к базовому, без учета хоста)

## P.S.
Для того, чтобы понимать, с какой частотой нужно читать документы из логброкера, чтобы распределение во времени было равномерным, а очередь ожидающих проверки документов не забилась из-за ограничения RPS, используется следующая эвристика: будем брать случайный документ, которого нет на поиске, каждые `index_timeout / (max_int_rps * allowable_error_sec)` секунд. Соответственно, если мы уверены, что большинство документов доезжают до поиска за время `t << index_timeout`, то мы можем позволить себе брать больше документов для повышения репрезентативности выборки, просто увеличив параметр `allowable_error_sec`.

Идея в том, что при `allowable_error_sec = 1` брать кол-во документов равное `max_int_rps` за отрезок времени `index_time`, чтобы очередь не забивалась.