# YT
## Особенности
* В основе лежат официальные библиотеки [inside-yt](https://a.yandex-team.ru/arc/trunk/arcadia/iceberg/inside-yt) и [ytclient](https://a.yandex-team.ru/arc/trunk/arcadia/yt/java/ytclient)
* Большая часть параметров задается через [service.yaml](../how_it_works/configuration/service_yaml.md) в блоке `modules.yt`.
  В остальных случаях можно донастроить через Spring конфигурацию в коде.
* Возможность создания и настройки нескольких клиентов

## Быстрый старт
1. Добавляем в `service.yaml` следующие настройки:
   ```yaml
   modules:
     yt:
       cluster: freud
   ```

2. Получаем токен [здесь](https://oauth.yt.yandex.net). Добавляем его в локальный проперти файл:
   ```
   mj.yt.token=<ваш токен>
   ```

   {% cut "Другой способ (не рекомендуется)" %}
   Токен можно задать и в `service.yaml`, главное не коммитить его в аркадию:
   ```yaml
   modules:
     yt:
       token: <token here>
       cluster: freud
   ```
   {% endcut %}

3. Инжектим себе в код бин `ru.yandex.inside.yt.kosher.Yt.class` и пробуем получить или записать какие-то данные в общий тестовый кластер [Freud](https://yt.yandex-team.ru/freud/).
   ```java
   @Service
   public class TestService {

       @Autowired
       private Yt yt;

       public void someMethod() {
           yt.tables().write(...);
       }
   }
   ```

{% note info %}

Не забывайте, что настройки можно осуществлять для разных окружений. Подробнее [тут](../how_it_works/configuration/environment.md).

{% endnote %}

Пример (не является рекомендованными настройками)
```yaml
modules:
  yt:
    heavyCommandsRetries: 1
    heavyCommandsTimeoutMillis: 3000
    acl:
      permissions:
        - erewew
        - rttggbcz
        - ewqeqwx
    clients:
      hume:
        async: true
        protocol: rpc
        cluster: hume
        heavyCommandsRetries: 2
        heavyCommandsTimeoutMillis: 2000
        atomicity: true
        rpc:
          compression:
            requestCodecId: Lz4
          options:
            channelPoolSize: 10
            pingTimeoutMillis: 1000
      hahn:
        cluster: hahn
        portoJava17: true
        specPatch:
          tretresc:
            wqxzz: oiyouy
            piopoi: qweq
          kjkh: ewqpok
        acl:
          permissions:
            - oipopoip
            - weeqqwe
            - nmbnm
      arnold:
        async: true
        cluster: arnold
```

## Работа с одним клиентом
### Конфигурирование
#### Настройка клиента
_Здесь подразумевается настройка клиента из библиотеки [inside-yt](https://a.yandex-team.ru/arc/trunk/arcadia/iceberg/inside-yt)._

- _modules.yt.async_ - _boolean_ параметр для переключения между синхронным и асинхронным клиентом. По умолчанию `false`, т.е. если не задавать этот параметр, создастся синхронный клиент.
- _modules.yt.protocol_ - _enum_ параметр для выбора протокола взаимодействия с YT. Возможны два варианта: `http` или `rpc`. По умолчанию используется `http`.

  {% note warning %}

  RPC протокол доступен только для асинхронного клиента

  {% endnote %}

- _modules.yt.cluster_ - _enum_ параметр для выбора кластера, с которым будет работать клиент. Список доступных кластеров представлен [здесь](https://yt.yandex-team.ru/).
- _modules.yt.token_ - токен для аутентификации. Получение токена описано [здесь](https://yt.yandex-team.ru/docs/description/common/auth).

Выше перечислены лишь основные параметры. С остальными параметрами можно ознакомиться [здесь](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/yt-properties/src/main/java/YtProperties.java).

##### Расширенные настройки
Некоторые параметры нет возможности задать через service.yaml (или проперти в случае использования стартера без MJ). Но эти параметры можно заполнить через Spring конфигурацию в коде.
Для настройки синхронного клиента есть адаптер [YtSyncConfigurerAdapter](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/yt-spring-boot-starter/src/main/java/configurer/sync/YtSyncConfigurerAdapter.java). Наследуемся от него, переопределяем только интересующие вас методы и добавляем бин в Spring конфигурацию в своем проекте.
Аналогичный адаптер есть и для асинхронного клиента - [YtAsyncConfigurerAdapter](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/yt-spring-boot-starter/src/main/java/configurer/async/YtAsyncConfigurerAdapter.java).

#### Настройка RPC клиента
- _modules.yt.rpc.*_ - в этом разделе можно настроить RPC клиента, поставляемого с библиотекой [ytclient](https://a.yandex-team.ru/arc/trunk/arcadia/yt/java/ytclient). Он автоматически интегрируется в основного асинхронного клиента из библиотеки [inside-yt](https://a.yandex-team.ru/arc/trunk/arcadia/iceberg/inside-yt).
Через проперти можно задать большинство возможных параметров, актуальный список находится [здесь](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/yt-properties/src/main/java/rpc/YtRpcProperties.java).

- _modules.yt.rpc.compression.*_ - параметры сжатия [список](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/yt-properties/src/main/java/rpc/RpcCompressionProperties.java).
- _modules.yt.rpc.bus-connector.*_ - параметры соединения [список](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/yt-properties/src/main/java/rpc/BusConnectorProperties.java).
- _modules.yt.rpc.clusters[0...n].*_ - задание нескольких (fallback) кластеров [возможные параметры каждого кластера](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/yt-properties/src/main/java/rpc/YtClusterProperties.java).
- _modules.yt.rpc.options.*_ - другие параметры (таймауты и прочее). [Список](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/yt-properties/src/main/java/rpc/RpcOptionsProperties.java).
- _modules.yt.rpc.custom_ - boolean параметр для создания кастомного бина [YtClient](https://a.yandex-team.ru/arc_vcs/yt/java/ytclient/src/main/java/ru/yandex/yt/ytclient/proxy/YtClient.java). Параметр нужен лишь для тех случаев, когда вы не задали ни одного кастомного параметра в блоке `modules.yt.rpc.*`. В такой ситуации бин YtClient создаваться не будет, а в основном клиенте будет использоваться дефолтная реализация. И в этой ситуации, если вам все таки нужен кастомный клиент, но который вы, например, хотите настроить через Spring конфигурацию в коде, или по другим причинам, то стоит установить значение для этого параметра `true`. В остальных ситуациях использовать этот параметр нет необходимости.

##### Расширенные настройки RPC клиента
Осуществляются через [YtRpcClientConfigurerAdapter](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/yt-spring-boot-starter/src/main/java/configurer/rpc/YtRpcClientConfigurerAdapter.java).

### Использование
Инжектим клиента в свой сервис и работаем с ним.
```java
@Service
public class UserService {

    @Autowired
    private Yt yt;
    
    public void save(User user) {
        yt.tables().write(...);
    }
}
```

{% note warning %}

Классы синхронного и асинхронного клиентов имеют одинаковые названия, но лежат в разных пакетах. Не перепутайте!
Синхронный клиент: `ru.yandex.inside.yt.kosher.Yt.class`
Асинхронный клиент: `ru.yandex.inside.yt.kosher.async.Yt.class`

{% endnote %}

Если вы создавали кастомного RPC клиента, то его тоже можно заинжектить в код:
```java
@Service
public class UserService {

    @Autowired
    private YtClient ytClient;

    private List<User> getUsers() {
        ytClient.lookupRows(...);
        ...
    }
}
```

## Работа с несколькими клиентами
### Конфигурирование
Конфигурирование происходит аналогичным образом, но есть ряд отличий.

В разделе `modules.yt.*` в данном случае задаются параметры, которые применятся ко всем клиентам.
А в разделах `modules.yt.clients.<id>.*` соответствующих id отдельного клиента, задаются специфичные настройки, которые в том числе могут переопределять значения параметров из общего блока.
`id` можно указывать любой. По нему потом будет осуществляться получение конкретного клиента в коде.
Схема свойств, как в блоке `modules.yt.*`, так и в блоках параметров конкретного клиента одинакова и равна той, что используется в [работе с одним клиентом](#работа-с-одним-клиентом) - [YtProperties](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/yt-properties/src/main/java/YtProperties.java).

На основе информации из `service.yaml` генерируется класс `ru.yandex.mj.generated.yt.YtClientId` с идентификаторами клиентов. С помощью него можно удобно получать нужного клиента или мапить конфигурационные бины.

#### Расширенные настройки нескольких клиентов
Осуществляются так же через [Configurer'ы](#расширенные-настройки), но чтобы смапить какой-либо конфигурационный бин на конкретного клиента, необходимо повесить на него аннотацию `@Qualifier` с указанием id клиента. id клиента не надо вспоминать и вводить в виде строки - id можно получить из статической переменной в классе `YtClientId`.
```java
@Qualifier(YtClientId.HAHN_CLIENT_ID)
@Bean
public YtAsyncConfigurer hahnYtAsyncConfigurer() {
    return new YtAsyncConfigurerAdapter() {
        @Override
        public EventLoopGroup getEventLoopGroup() {
            return new NioEventLoopGroup();
        }
    };
}
```

### Использование
Получить клиентов можно с помощью [YtProvider](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/mj/v1/mj-yt/src/main/java/provider/YtProvider.java), независимо от того синхронный клиент или асинхронный. При получении используем класс `YtClientId`.
```java
@Service
public class UserService {

    @Autowired
    private YtProvider ytProvider;
    
    public void save(User user) {
        ytProvider.get(YtClientId.HAHN).tables().write(...);
    }
}
```

## Стартер
Предназаначен для быстрого подключения **YT** в любой проект на **Spring Boot**. Конфигурирование и использование осуществляется как в MJ, за некоторыми исключениями, о которых ниже.

### Установка
Добавить в `ya.make` зависимость:
```
market/infra/java-application/spring-boot-starters/yt-spring-boot-starter
```

### Конфигурирование
Доступны все те же проперти, что есть в MJ, только вместо раздела `modules.yt.*` используется проперти `mj.yt.*`.

### Работа с несколькими клиентами
#### Расширенные настройки нескольких клиентов
Осуществляются так же через [Configurer'ы](#расширенные-настройки), но чтобы смапить конфигурер к нужному клиенту, используется [YtConfigurersHolder](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/yt-spring-boot-starter/src/main/java/configurer/YtConfigurersHolder.java).
**Пример**
Хотим установить клиенту с id _"hahn-client"_ кастомный `EventLoopGroup`:
```java
@Bean
public YtConfigurersHolder ytConfigurersHolder() {
    final YtConfigurersHolder ytConfigurersHolder = new YtConfigurersHolder();
    final YtAsyncConfigurerAdapter hahnClientConfigurer = new YtAsyncConfigurerAdapter() {
        @Override
        public EventLoopGroup getEventLoopGroup() {
            return new NioEventLoopGroup();
        }
    };
    ytConfigurersHolder.setYtAsyncConfigurers(Map.of("hahn-client", hahnClientConfigurer));
    return ytConfigurersHolder;
}
```

{% note info %}

В MJ фреймворке это делается проще! Не надо создавать `YtConfigurersHolder%`. Чтобы смапить какой-либо конфигурационный бин на конкретного клиента, необходимо повесить на него аннотацию `@Qualifier` с указанием id клиента. Подробнее ((https://wiki.yandex-team.ru/market/development/developer-experience/mj-framework/mj-yt-module/#4.uproshhennyjjmappingkonfiguracionnyxbinovkkonkretnomuklientu тут)).

{% endnote %}

#### Использование
Получение клиентов в коде осуществляется через бины-провайдеры по id клиентов, задаваемых через проперти.
Синхронных клиентов получаем через [YtSyncProvider](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/yt-spring-boot-starter/src/main/java/provider/sync/YtSyncProvider.java), асинхронных - через [YtAsyncProvider](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/yt-spring-boot-starter/src/main/java/provider/async/YtAsyncProvider.java).
Получение кастомных RPC клиентов из библиотеки [ytclient](https://a.yandex-team.ru/arc/trunk/arcadia/yt/java/ytclient) осуществляется через [YtRpcClientProvider](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/spring-boot-starters/yt-spring-boot-starter/src/main/java/provider/async/YtRpcClientProvider.java).

Пример
```java
@Service
public class UserService {

    @Autowired
    private YtSyncProvider ytSyncProvider;

    @Autowired
    private YtAsyncProvider ytAsyncProvider;
    
    public void save(User user) {
        ytSyncProvider.get("hahn-client").tables().write(...);
        ytAsyncProvider.get("arnold-client").tables().write(...);
    }
}
```

{% note info %}

В MJ фреймворке это делается проще! Есть единый `YtProvider`, который возвращает как синхронных, так и асинхронных клиентов. Подробнее [тут](https://wiki.yandex-team.ru/market/development/developer-experience/mj-framework/mj-yt-module/#3.edinajatochkapoluchenijaytklientov).

{% endnote %}

## Ваш фидбек
На данный момент модуль и стартер имеют базовый функционал и подготовлены для дальнейшего расширения. Предложения по добавлению новых функций приветствуются - приходите к нам в [чат](https://t.me/joinchat/RImGNXqbohFkOTg6) или пишите в [этот тикет](https://st.yandex-team.ru/MARKETDX-643).