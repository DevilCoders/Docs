## Резолвер и балансер для grpc-клиента

При создании grpc-соединения возникают, среди прочих, такие типовые задачи:

- получить для заданного сервиса список актуальных хостов (эту задачу решает резолвер)
- выбрать хост для отправки очередного grpc-запроса (эту задачу решает балансер)

## YP-резолвер

YP-резолвер получает на вход имя сервиса (напрмер, ```travel-notifier-testing.api```) и запрашивает у YP service discovery
список хостов для данного сервиса.

Чтобы воспользоваться резолвером, нужно построить для него билдер и передать в grpc.Dial(...):
```
import ypresolver "a.yandex-team.ru/travel/library/go/grpcutil/client/ypresolver"

gConn, err := grpc.DialContext(
	ctx,
	ypresolver.BuildServiceFQDN("travel-notifier-testing.api"),
	grpc.WithResolvers(ypresolver.NewYPResolverBuilder()),
    // прочие, не связанные с резолвером, опции grpc-вызова
	grpc.WithInsecure(),
	grpc.WithBlock(),
)
```

Резолвер предполагает, что может установить незащищённое соединение с [YP service discovery host](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/golang/resolver/resolver.go?rev=7661833#L9) без дополнительных credentials, более сложные способы
установить соединение с YP service discovery пока не поддерживаются.

### Опции YP-резолвера

Опция | Описание
--- | --- 
```WithLogger(l log.Structured)``` | Резолвер будет использовать указанный логгер. Нужен log.Structured, а не просто log.Logger, этого требует резолвер [YP service discovery](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/golang/resolver/grpcresolver/resolver_opts.go?rev=r7662050#L24)
```WithConnectionTimeout(timeout time.Duration)``` | Максимальное время на установку соединения с YP service discovery
```WithClusters(clusters []string)``` | Будут использованы только дата-центры [(sas/vla/man/iva/myt)](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/golang/resolver/resolver.go?rev=r7662050#L13) из заданного списка.

## Статический резолвер

Нужен только для fall-back сценариев, когда нет возможности получать список хостов сервиса через дискавери. Получает на вход список
хостов, и его же и отдаёт:

```
import staticresolver "a.yandex-team.ru/travel/library/go/grpcutil/client/static_resolver"

gConn, err := grpc.DialContext(
	ctx,
	"static:///host1:9001,host2:9002,host3:9003",
	grpc.WithResolvers(staticresolver.NewStaticResolverBuilder()),
    // прочие, не связанные с резолвером, опции grpc-вызова
	grpc.WithInsecure(),
	grpc.WithBlock(),
)
```

```static``` - название схемы в адресе сервиса, именно оно определяет, какой резолвер будет использован при grpc-вызове; у каждого резолвера (из числа одновременно зарегистрированных) - своё название схемы. Название схемы можно получить из константы ```staticresolver.StaticScheme```.


## Балансер с проверкой health-check

Балансер выбирает, на какой хост отправить следующий grpc-запрос. Работает по следующему алгоритму:

- выполняем health-check в фоне для всех известных хостов сервиса
- как в round_robin, выбираем следующий по списку хост 
- если хост is serving, отдаём этот хост в качестве ответа, иначе пробуем следующий по списку, пока не найдём is serving

Можно указать балансеру интервал времени, в течение которого не следует переопрашивать хосты - чтобы не создавать на них ненужную нагрузку.

В случае, если балансеру не удалось найти is serving хост, будет выдана ошибка при rpc-вызове (неприятный момент,
to be fixed later: сейчас ошибка выдаётся только по истечении заданного для grpc.DialContext(...) таймаута, хотя об отстутствии
подходящего хоста балансеру известно гораздо раньше).

Также ошибка при rpc-вызове может быть выдана, если балансер не переопросил какой-либо хост (т.к. заданный интервал переопроса 
не истёк), и хост, ранее помеченный балансером как is serving, перестал быть таковым.

За вычетом health-check проверки, балансер работает как обычный round_robin, поэтому можно вместо него round_robin и использовать:

```
gConn, err := grpc.DialContext(
	ctx,
	ypresolver.BuildServiceFQDN("service"),
    grpc.WithDefaultServiceConfig(
        `{"loadBalancingPolicy":"round_robin", "healthCheckConfig": {"serviceName": "travel-notifier-api"}}`),
    // прочие, не связанные с балансером, опции grpc-вызова
	grpc.WithInsecure(),
	grpc.WithBlock(),
)
```

Важно: в healthCheckConfig указывается не имя сервиса в service-discovery, а имя сервиса, для которого на grpc-сервере
зарегистрирован health-server [(пример)](https://a.yandex-team.ru/arc/trunk/arcadia/travel/notifier/cmd/notifier/main.go?rev=r7662123#L35). Если каждый инстанс сервиса (каждый grpc-сервер) располагается на отдельном хосте, healthCheckConfig
можно не указывать:

```
    grpc.WithDefaultServiceConfig(`{"loadBalancingPolicy":"round_robin"`),
```

Чтобы использовать балансер с health-checkом, требуется выполнить следующие шаги:

Шаг 1. Зарегистрировать балансер в пакетном методе init():

```
import (
	corelog "a.yandex-team.ru/library/go/core/log"
	"a.yandex-team.ru/library/go/core/log/zap"
	hcbalancer "a.yandex-team.ru/travel/library/go/grpcutil/client/healthcheck_balancer"
	"google.golang.org/grpc/balancer"
)

func init() {
	logger, _ := zap.NewDeployLogger(corelog.DebugLevel)
	balancer.Register(
		hcbalancer.NewBalancerBuilder(
			hcbalancer.NewHealthCheckPickerBuilder(
				hcbalancer.WithLogger(logger),
				hcbalancer.WithHealthCheckInterval(time.Duration(10*time.Second)),
			),
		),
	)
}
```

Шаг 2. Использовать название балансера ```healthcheck_balancer``` при grpc-вызове:

```
gConn, err := grpc.DialContext(
	ctx,
	"scheme:///service",
    grpc.WithDefaultServiceConfig(`{"loadBalancingPolicy":"healthcheck_balancer"`),
    grpc.WithDisableHealthCheck(),
    // прочие, не связанные с балансером, опции grpc-вызова
	grpc.WithInsecure(),
	grpc.WithBlock(),
)
```

Замечание. Если grpc не находит нужного балансера, он использует "pick first" балансер, который всегда выбирает самый первый хост
(возможно, в будущем это исправят).
Поэтому лучше использовать ```hcbalancer.BalancerName``` в качестве loadBalancingPolicy, чтобы минимизировать риск опечаток.

При использовании hcbalancer важно также использовать grpc.WithDisableHealthCheck(), иначе health-checkи балансера и самого grpc
будут конфликтовать (особенно, если в hcbalancer используется опция WithHealthCheckServiceNameFunc - см. описание опций ниже).

### Опции hc-балансера

Опция | Описание
--- | --- 
```WithLogger(l log.Logger)``` | Балансер будет использовать указанный логгер.
```WithHealthCheckTimeout(timeout time.Duration)``` | Максимальное время на проверку health-check для одного хоста
```WithHealthCheckInterval(interval time.Duration)``` | Повторять проверку health-check для каждого хоста через указанный интервал.
```WithHealthyStateTimeout(interval time.Duration)``` | Если после успешной health-check проверки, эту проверку по каким-либо причинам не удаётся повторить, хост будет считаться healthy в течение указанного интервала времени.
```WithHealthCheckServiceName(healthCheckServiceName string)``` | Имя сервиса для health-checkа. Как и в healthCheckConfig выше, может не совпадать с именем сервиса в health-discovery. Для случая, когда каждый grpc-сервер расположен на отдельном хосте, должно быть можно не указывать эту опцию.
```WithHealthCheckServiceNameFunc(fn HealthCheckServiceNameFunc)``` | Только для тестирования - чтобы тестировать клиента со стендом grpc-серверов, поднятых локально, в рамках одного процесса, сервисы для health-checkа у этих серверов должны отличаться (иначе health-check не работает)

В папке example - пример работающего клиента для сервиса ```travel-notifier-testing.api```.
