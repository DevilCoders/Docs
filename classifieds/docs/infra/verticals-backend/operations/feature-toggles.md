# Использование фича-флагов

## Рекомендованный способ

Рекомендуется использовать [централизованное решение](https://docs.yandex-team.ru/classifieds-infra/tools/feature-toggles) для фича-флагов.
Для удобства написан [общий клиент](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/common/clients/feature-toggles).

Пример использования:

```scala
override def makeEnv: ZLayer[BaseEnvironment, Throwable, Env] = ZLayer.wire(
  ...,
  Pureconfig.loadLayer[DefaultFeatureTogglesClient.Config]("feature-toggles"),
  FeatureTogglesClient.live
)

...

val useNewFeatures: Feature[Boolean] = Feature[Boolean]("use_new_features", false)
...
client.get(useNewFeatures)

```

В манифесте деплоя указать ссылку на API:

```
FEATURE_TOGGLES_HOST: ${host:feature-toggles-api:grpc}
```

## Легаси-решение на Zookeeper

### Конфигурация

Фича-флаги хранятся в зоокипере, поэтому в первую очередь надо подключить его к
своему сервису.

```
# connect-string подставит шива из переменной окружения _DEPLOY_ZOOKEEPER_CONN_STRING
zookeeper {
  group-prefix = "auto/autoru-match-maker"
  auth {
    user = auto
    password = ${?ZK_PASSWORD}
  }
}
```

Для API переключения фича-флагов по умолчанию используется порт 7000. Если
нужно его поменять, можно прописать
```
features.toggle.grpc.port = 9999
```

В карте сервисов нужно открыть порт наружу:

```
  - name: feature-toggle
    protocol: grpc
    port: 7000
    description: grpc api for feature toggles
```

### Инициализация API переключения фича-флагов

> Для _использования_ фич это делать не обязательно. Дальнейшие действия нужны
> только чтобы получить API _переключения_ флагов.

В `Main.scala` переопределить `program` и добавить в него вызов
`FeatureToggleServer.run`. Environment приложения при этом
должен содержать `Features with Configuration with Tracing with Logging`.
Пример:

```scala

object Main extends BaseApp {

  override type Env = Tracing with Configuration with Features with Logging

  override def makeEnv: ZLayer[BaseEnvironment, Throwable, Env] = ???

  override def program: ZIO[Env, Throwable, Any] =
    FeatureToggleServer.run *>
      ZIO.collectAllPar(List(???))
}

```

### Переключение

Проще всего использовать [grpcui](https://github.com/fullstorydev/grpcui):

```
grpcui -plaintext match-maker-scheduler-feature-toggle.vrts-slb.test.vertis.yandex.net:80
```
