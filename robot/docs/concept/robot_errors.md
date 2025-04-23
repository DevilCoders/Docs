# Коды ошибок Робота

При обращении к каждому урлу поисковой робот сохраняет код ответа сервера или код ошибки. Полный [список кодов есть в CVS](http://tree.yandex.ru/cgi-bin/cvsweb.cgi/arcadia/util/httpcodes.h?rev=1), на этой странице приведена расшифровка нестандартных кодов. Интерпретация стандартных кодов есть в [описании http 1.1](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10).

## Ошибки протокола (документ не скачивается и не обрабатывается) / Protocol Errors (the document could not be downloaded and processed)

Название ошибки|Код ошибки|Описание|English description
:--- | :---| :---| :---
**HTTP_BAD_RESPONSE_HEADER**|1000|не используется |**not used**
**HTTP_CONNECTION_LOST**|1001 |обрыв коннекта |Connection was lost
**HTTP_BODY_TOO_LARGE**|1002 |размер текста превышает заданный предел |The document's body text exceeds the limit
**HTTP_ROBOTS_TXT_DISALLOW**|1003|документ запрещен в robots.txt |The document is disallowed in robots.txt
**HTTP_BAD_URL**|1004 |адрес документа не соответствует стандарту |The URL does not meet the standards
**HTTP_BAD_MIME**|1005 |сервер отдает не указывает или не правильно указывает формат сообщения или указывает формат, который нами не индексируется |The server does not specify the message format. Or specifies it incorrectly. Or specifies a format we do not support.
**HTTP_DNS_FAILURE**|1006 <br/>У Zora есть кеширующий DNS-прокси с таким принципом работы:<br/>при запросе идём в НОКовский dns (ns-cache.yandex.net и dns-cache.yandex.net);<br/>- если нам вернулся хороший статус, отдаём его в ответе и складываем в кеш;<br/>- если нам вернулся NXDOMAIN (хороший статус о том, что хоста не существует), отдаём его в ответе и складываем в кеш;<br/>- если нам вернулся плохой ответ (таймаут, SERVFAIL и т.п.), то достаём статус из кеша и отдаём его в ответе;<br/>- если в кеше ничего нет, отдаём плохой ответ (аналог SERVFAIL)|Ошибка DNS|DNS error
**HTTP_BAD_STATUS_CODE**|1007 |статус код не соответствует стандарту |Non-standard HTTP status code was returned
**HTTP_BAD_HEADER_STRING**|1008 |http-заголовок не соответствует стандарту (нашему расширению) |Non-standard HTTP header string (does not meet our extension requirements)
**HTTP_BAD_CHUNK**|1009 |не правильно указан размер chunk'а |Chunk size specified incorrectly
**HTTP_CONNECT_FAILED**|1010 |не удалось соединиться с http-сервером |Connection failed (the crawler failed to establish connection with the server)
**HTTP_FILTER_DISALLOW**|1011 |адрес запрещен фильтром |The address disallowed in filter
**HTTP_LOCAL_EIO**|1012 |внутренняя ошибка робота |The crawler's inner failure
**HTTP_BAD_CONTENT_LENGTH**|1013 |не указана или неправильно указана длина сообщения (в тех случаях, когда это необходимо) |Incorrect message length (in cases when this parameter is necessary)
**HTTP_BAD_ENCODING**|1014 |не правильно задан заголовок transfer-encoding или указан не известный нам тип |The unknown or incorrectly specified transfer-encoding
**HTTP_LENGTH_UNKNOWN**|1015 |не указана или неправильно указана длина сообщения (в тех случаях, когда это необходимо) |Incorrect message length (in cases when this parameter is necessary)
**HTTP_HEADER_EOF**|1016 |передача данных закончилась во время передачи http-заголовков |Data transfer stopped while transferring HTTP headers
**HTTP_MESSAGE_EOF**|1017 |передача данных закончилась во время передачи текста сообщения (возможно, неправильно указана длина)|Data transfer stopped while transferring the message text (most likely due to incorrectly specified message size)
**HTTP_CHUNK_EOF**|1018 |передача данных закончилась во время передачи chunk'а |Data transfer stopped while transferring a chunk
**HTTP_PAST_EOF**|1019 |передача данных продолжается после передачи текста сообщения (возможно, неправильно указана длина)|Data transfer continues after receiving the whole message (most likely due to incorrectly specified message size)
**HTTP_HEADER_TOO_LARGE**|1020 |длина http-заголовков превысила предел |HTTP headers' length exceeds limit
**HTTP_URL_TOO_LARGE**|1021 |длина адреса превысила предел |URL length exceeds limit
**HTTP_INTERRUPTED**|1022 |робот был остановлен во время скачивания документа |The crawler was stopped (turned off) while downloading the document
**HTTP_CUSTOM_NOT_MODIFIED**|1023|документ не изменился с последнего обхода (проверяется по содержимому, используется пока только в картинках) |The document has not changed since the last visit (used only in Images)
**HTTP_BAD_CONTENT_ENCODING**|1024|роботу прислали неверный content-encoding (например, просили несжатые данные, а прислали сжатый gzip поток) |The crawler was given a wrong content encoding (e.g. we asked for uncompressed data, but have received a compressed GZIP stream)
**HTTP_NO_RESOURCES**|1025 | |//no description//
**HTTP_FETCHER_SHUTDOWN**|1026 | |//no description//
**HTTP_CHUNK_TOO_LARGE**|1027 |размер chunk'а превысил предел |Chunk size exceeds limit
**HTTP_SERVER_BUSY**|1028 |удаленный сервер вернул ошибку (скорее всего, 5xx) |The server returned an error code (most likely a 5xx code)
**HTTP_SERVICE_UNKNOWN**|1029 |Неизвестное имя источника для спайдера/зоры|Service is unknown
**HTTP_PROXY_UNKNOWN**|1030 |неопределённая ошибка zora |An unidentified zora error
**HTTP_PROXY_REQUEST_TIME_OUT**|1031 |превышен timeout запроса при обработке в zora |A timeout error while the request was processed at the zora
**HTTP_PROXY_INTERNAL_ERROR**|1032 |ошибка zora при обработке запроса |zora error occurred while the request was processed
**HTTP_PROXY_CONNECT_FAILED**|1033 | не удалось соединиться с proxy | Connection to proxy failed
**HTTP_PROXY_CONNECTION_LOST**|1034 | соединение с proxy оборвалось | Connection to proxy is lost
**HTTP_PROXY_NO_PROXY**|1035 | в запрашиваемом регионе нету proxy | No proxy in requested region
**HTTP_PROXY_ERROR**|1036 |Ошибка промежуточной прокси (squid)|Spider proxy returned custom error
**HTTP_SSL_ERROR**|1037 |Ошибка SSL (для https-хостов) | Ssl error (for https-hosts) 
**HTTP_CACHED_COPY_NOT_FOUND**|1038|Для запросов типа "only from cache" - документ не найден в кэше|Document not found in spider cache - for "only-from-cache" requests
**HTTP_TIMEDOUT_WHILE_BYTES_RECEIVING**|1039|не используется|not used
**HTTP_FETCHER_BAD_RESPONSE**|1040|внутренняя ошибка: неожиданный ответ от фетчера|internal error: unexpected response from fetcher
**HTTP_FETCHER_MB_ERROR**|1041|внутренняя ошибка: ошибка коммуникации с фетчером|internal error: error in communication with fetcher
**FS_SSL_CERT_ERROR**|1042|Ssl сертификат не является доверенным |Ssl certificate is untrusted
**FS_FIREWALL_REJECT**|1043|Адрес из внутренней сети запрещен для скачивания файрволом|Internal network address is rejected by firewall


## Ошибки возникающие при обработке загруженного документа (сервер возвратил код 200) / Processing Errors (The document was downloaded, but could not be processed)

Название ошибки|Код ошибки|Описание|English description
:--- | :---| :---| :---
**EXT_HTTP_MIRRMOVE**|2000 | документ перенесен с зеркала|The document has recently been moved from a previous primary mirror site (after the new primary mirror was chosen). Once the document is re-visited by the crawler, it will receive the code **200** again.
**EXT_HTTP_NOTUSED1**|2001 | в настоящее время не используется, но такие коды могли сохраниться|**not used**, though several documents might have received this code in the past
**EXT_HTTP_NOTUSED2**|2002 | не используется|**not used**
**EXT_HTTP_NOTUSED3**|2003 | не используется|**not used**
**EXT_HTTP_REFRESH**|2004 | документ содержит мета-тег refresh|The document contains a Refresh meta tag
**EXT_HTTP_NOINDEX**|2005 | документ содержит мета-тег noindex|The document contains a Noindex meta tag
**EXT_HTTP_BADCODES**|2006 | кодировка документа не распознана|The document's encoding could not be identified
**EXT_HTTP_SITESTAT**|2007 | по одной из эвристик документ является логами сервера|The document was identified as a server log by one of the heuristics
**EXT_HTTP_IOERROR**|2008 | внутренняя ошибка робота (не бывает)|The crawler's inner error **(does not occur)**
**EXT_HTTP_BASEERROR**|2009 | внутренняя ошибка робота (не бывает)|The crawler's inner error **(does not occur)**
**EXT_HTTP_PARSERROR**|2010 | ошибка парсера, например, документ имеет неправильный формат|The parser's error (due to incorrect format of the document etc.)
**EXT_HTTP_BAD_CHARSET**|2011 | кодировка документа не распознана, например **если он не содержит текста или содержит текст в различных кодировках**|The encoding could not be identified (due to absence of text or usage of several encodings on the same page)
**EXT_HTTP_BAD_LANGUAGE**|2012|язык документа не распознан, либо не поддерживается (татарский, чешский,...)|Unidentified or unsupported language (Tatar, Czech, etc)
**EXT_HTTP_NUMERERROR**|2013 | внутренняя ошибка робота (не бывает)|The crawler's inner error **(does not occur)**
**EXT_HTTP_EMPTYDOC**|2014 | документ не содержит текста|The document contains no text
**EXT_HTTP_HUGEDOC**|2015 | текст документа или его внутреннее представление превышает предел|The document is too large
**EXT_HTTP_LINKGARBAGE**|2016 | слишком много ссылок|Too many links in the document
**EXT_HTTP_EXDUPLICATE**|2017 | URL признан дублем. Код не встречается в обходах Зоры, но может отображаться в filterstate Самовара, когда база Юпитера посылает сигнал о признании страницы дублем|URL is dublicate of another URL. This code is not used by Zora, but can be used in Samovar filterstate if Jupiter search base send the signal that the url is a duplicate
**EXT_HTTP_FILTERED**|2018 | код ошибки, который появится в будущем -- случай, когда сайт был проиндексирован, а потом забанен фильтром; сейчас код используется неправильно, эту ошибку исправят|The site was indexed and then banned in filter. **At this moment the code is used incorrectly**, the mistake will be fixed soon.
**EXT_HTTP_PARSERFAIL**|2019 | внутренняя ошибка парсера (упал парсер) |The parser's failure 
**EXT_HTTP_GZIPERROR**|2020 | не распаковывается пришедший нам gzip- или deflate-поток|The received GZIP or DEFLATE stream could not be extracted
**EXT_HTTP_CLEANPARAM**|2021 | урл зафильтрован за незначащие параметры |The URL contains meaningless extra parameters which do not affect the way the page (and its content) is displayed (kinda duplicate URL)
**EXT_HTTP_MANUAL_DELETE_URL**|2022| команда извне на удаление урла (используется только в картинках, дается линковой базой) |The URL was deleted following an external command (used only in Images, the command is given by a Link database - ?)
**EXT_HTTP_CUSTOM_PARTIAL_CONTENT**|2023|генерируется спайдером для документов, которые сам спайдер не считает нужным считывать целиком (нет смысла считывать весь документ, если индексируемая информация расположена в начале и ее не много по сравнению с полным размером контента). Документ скачивается частично, и индексируется необходимая часть документа.|Given to documents that should not be downloaded in their entirety (there's no sense to download the whole document if the actual information is located in the beginning and takes a small part of the whole document's size). The document is downloaded partially and the necessary information is indexed.
**EXT_HTTP_EMPTY_RESPONSE**|2024 | нулевой ответ сервера (т.е. 0 байт), не путать с 2014, когда ненулевой ответ не содержит текст |The server returns zero response (0 bytes). Not to be confused with **2014**.
**EXT_HTTP_REL_CANONICAL**|2025 | урл не является каноническим (содержит rel="canonical") и его канонический урл проиндексирован |The URL is non-canonical, but it contains %%rel="canonical"%% and its' canonical version has already been indexed


## Ошибки 3xxx (filtered) / 3xxx errors (filtered)

Название ошибки|Код ошибки|Описание|English description
:--- | :---| :---| :---
**EXT_HTTP_HOSTFILTER**|3001 | хост запрещен |The domain is in filter
**EXT_HTTP_URLFILTER**|3002 | запрещен данный путь, или его префикс |The URL (or its prefix) is in filter
**EXT_HTTP_SUFFIXFILTER**|3003 | зафильтрован по расширению (например, jpg, mp3)|The URL is filtered for file extensions (e.g. jpg, mp3, etc.)
**EXT_HTTP_DOMAINFILTER**|3004 | домен запрещен |The domain is in filter
**EXT_HTTP_EXTDOMAINFILTER**|3005 | домен не разрешен - по умолчанию |The domain is in filter
**EXT_HTTP_PORTFILTER**|3006 | хост запрещен с данным портом, при этом для данного хоста указан еще хотя бы один порт |The domain is forbidden for indexing through this port (but there should be at least one more port specified for this domain)
**EXT_HTTP_MIRROR**|3007 | неглавное зеркало |The URL belongs to a secondary mirror
**EXT_HTTP_DEEPDIR**|3008 | **не используется**, по всей видимости - слишком много директорий в пути |**not used**
**EXT_HTTP_DUPDIRS**|3009 | **не используется**, слишком много повторений директорий в пути|**not used**
**EXT_HTTP_REGEXP**|3010 | запрещен rfl фильтром |The document is filtered in RFL
**EXT_HTTP_OLDDELETED**|3012 | имеет статус deleted более полутора месяцев |The document has had the 'deleted' status for more than 1,5 months
**EXT_HTTP_PENALTY**|3013 | зафильтрован за пенальти, давно не отвечает или что-нибудь в этом роде, --морды попадать не должны-- |The document is filtered for penalty (does not answer for a long time or something like that). --Main pages should not receive this code--
**EXT_HTTP_HUGEHOST**|3014| статус не indexed и не duplicate, большой хост (больше 1.5 * 10^6 документов в данный момент) |The number of URLs indexed at this domain has already exceeded the limit (1,5*10^^6^^), and any extra documents receive this error code instead of being indexed
**EXT_HTTP_POLICY**|3015 | **используется в быстром**, в большом не используется - запрещен политикой текущего робота |The document is forbidden by the crawler's current policy **(used in fast bot only)**
**EXT_HTTP_TOOOLD**|3016 | **не используется, по всей видимости**, давно не переобходится |The document has not been re-visited since forever. **[apparently] not used**
**EXT_HTTP_GARBAGE**|3017 | выставляется незаэнкоженным урлам. Может кому-то еще|The URL contains non-latin symbols which weren't encoded properly (e.g. plain cyrillic symbols mixed with latin ones). The code may probably be given in some other cases as well.
**EXT_HTTP_FOREIGN**|3018 | хост принадлежит другому сегменту, в правильной базе такого быть не должно |The document was saved to a different walrus than the rest of documents from this domain. Such situations should never occur in a correct database.
**EXT_HTTP_EXT_REGEXP**|3019 | **не используется**, для stonesilter |**not used**, reserved for **stonesfilter**
**EXT_HTTP_HOPS**|3020 | фильтрация по хопам в rfl фильтре |Filtered in RFL for (too many?) hops ++(A number of hops is a number of clicks one has to make to get to this page from the main page)++
**EXT_HTTP_SELRANK**|3021 | фильтрация по selectionRank |The document is filtered by SelectionRank
**EXT_HTTP_NOLINKS**|3022 | фильтрация урлов без внешних ссылок(сейчас определен для урлов-источников ссылок) |The URL does not have external links (defined for link sources) 
**EXT_HTTP_WRONGMULTILANG**|3023 | неправильный мультиязычный хост. Хранится как мультиязычный, но в базе его нет. |Wrong multilanguage host (@tur, @us and e.c.)
**EXT_HTTP_SOFTMIRRORS**|3024 | | 
**EXT_HTTP_BIGLEVEL**|3025 | фильтрация урлов с хостов на больших доменах (> 6) |The host of URL has too big domain level (more than 6) 


## Ошибки 4xxx, быстрый робот / 4xxx errors, fast bot

Название ошибки|Код ошибки|Описание|English description
:--- | :---| :---| :---
**EXT_HTTP_FASTHOPS**|4000 | Урл не обходить |Do not visit this URL
**EXT_HTTP_NODOC**|4001 | Нет документа на урле |No document exists for this URL

----
## Ошибки 5xxx, politeness / 5xxx politeness
В этом разделе под лимитами понимается общее для Яндекса ограничение на рейт к ip/хосту. Исключение - если у источника выделенная группа лимитов.

Название ошибки|Код ошибки|Описание|English description
:--- | :---| :---| :---
**FS_SCH_IP_BUSY**| 5100 | Превышен лимит на скачивание с ip | ip limit exceeded 
**FS_SCH_HOST_BUSY**| 5101 | Превышен лимит на скачивание с хоста | host limit exceeded 
**FS_SCH_HOST_RENEWED_RECENTLY**| 5102 | Хостовый объект ещё не инициализирован (не скачан robots и т.п.) | host is not initialized yet 

## Ошибки 7xxx, zoracl / 7xxx zoracl

Название ошибки|Код ошибки|Описание|English description
:--- | :---| :---| :---
**FS_ZORACL_DUPLICATE**| 7000 | Дубликат во входящих данных zoracl | Zoracl: request was discarded as duplicate 
**FS_ZORACL_PRIORITIZED**| 7001 | | Zoracl: request was pushed out by other request with higher priority 

## Хостовые состояния / Host statuses

Помимо ошибок для отдельных страниц, существует также набор статусов для доменного имени целиком. К примеру, если все запросы к сайту блокируются с кодом 1010, то весь домен будет недоступен. Полный список состояний можно найти ниже.

Название статуса|Код статуса|Описание|English description
:--- | :---| :---| :---
OK|0||
FINISHED|1|Статус 200 ОК, хост доступен. Важно учесть, что такой код не означает доступность всех страниц, а доступность хоста к посещению. Даже если все страницы будут отдавать 403 код, хост все еще будет считать доступным.|Status 200 OK, the host is available. Note that this doesn't mean all the pages are avaiable. Even if all the pages responds with http-code 403, the domain will be considered as available.
TERMINATED|2||
HUGE_QUEUE|3||
BUSY|4|Сервер загружен и не может обработать запросы робота. Например, на все запросы отдаются коды 5XX| The server is overloaded and cannot process requests. For example, all responses are 5XXs.
CONNECT_LOST|5||
DISALLOWED|6||
SUBS_CONNECT_FAILED|7||
HUGE_ROBOTS|10||
BAD_ROBOTS|11||
DNS_ERROR|12||
TEMP_DNS_ERROR|13||
CONNECT_FAILED|14||
RECLUSTER_FAKE|15||
DNS_SPAM|16||
SSL_CONNECTION_ERROR|17||
UNINITIALIZED|20||
CONNECT_LOST_INIT|21||
BUSY_DONTRY|22||
OK_INIT|23||
