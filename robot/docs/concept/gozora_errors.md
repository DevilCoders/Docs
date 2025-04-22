## Ошибки GoZora

По возможности используются стандартные коды ошибок http proxy (например, 502 Bad Gateway — не удалось установить соединение с удалённым хостом). Для всех нестандартных ошибок используется код 599 с хедером **X-Ya-GoZora-Error-Code**, в котором содержится дополнительный код ошибки. Этот набор ошибок по коду может пересекаться с [роботными ошибками](https://docs.yandex-team.ru/robot/concept/robot_errors), но обозначать другую проблему. Ошибки с их описанием можно найти в [конфиге](https://a.yandex-team.ru/arcadia/robot/zora/gozora/internal/zerrors/errors.go).


Название ошибки|Код ошибки|Описание|English description
:--- | :---| :---| :---
**InsecureConnection**|1000 |Запрашиваемый ресурс не прошел проверку сертификата безопасности |The remote host certificate verification failed
**DeniedByFirewall**|1001|Файрволл сайта отказал в доступе к запрашиваему ресурсу |the firewall system has denied access to remote host
**ClientHandshake**|1002 |Не удалось установить TLS-соединение с хостом |Failed to establish TLS connection with client
**TvmAuthorization**|1003|Авторизация по TVM не удалась |TVM authorization failed
**HostSplit**|1004 |Не удалось определить хост и порт в указанном URL'е |Failed to split host and port in destination url
**DnsResolveFailed**|1005 |DNS-резолв не удался (DNS сайта недоступны) |DNS resolve has failed
**DialFailed**|1006 |Не удалось установить связь с запрашивамым ресурсом |Host dial has failed
**RemoteUpgradeTlsFailed**|1007 |Это ошибка установки TLS-соединения с удалённым хостом. |Remote Upgrade Tls Failed
**ReadResponseFailed**|1008 |Возникла ошибка при чтении ответа удалённого хоста |Failed to read response from remote server
**RpsLimitExceeded**|1009 |Превышел лимит аккаунта на число запросов |Rps limit for the user has been exceeded
**RedirectFailed**|1010 |Возникл ошибка при следовании по редиректам. В хедере будет более конкретное описание ошибки |Redirect has failed for some reason
