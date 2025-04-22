# Spring в МДМ

{% note info %}

Здесь представлена выдержка с необходимым минимумом из [правил работы со Spring](https://wiki.yandex-team.ru/market/mbo/development/spring/) в Бэкофисе Маркета.

{% endnote %}

В компонентах службы контента Маркета мы используем Spring Context для инициализации приложения (создания и связи между собой различных объектов приложения). Также в новых компонентах используется Spring Boot для автоматического создания части бинов, без необходимости их явно описывать в Spring контексте.

Spring позволяет сконфигурировать контекст приложения многими способами - XML, Annotation, Java Config. Рекомендуется использовать только Java конфиги. Существующие XML/Annotation конфигурации нужно по возможности переводить на Java. Плюсы Java конфигов следующие:
1. Частичная проверка корректности конфигурации в процессе написания кода — конфиг классы компилируются вместе с остальными, ошибки подсвечиваются в IDE.
2. Почти полностью работает навигация и рефакторинг IDE.
3. В классах, реализующих бизнес логику, не нужны лишние Spring аннотации — легче создать кастомную версию с нужными зависимостями, например, для тестов.

## Рекомендации по созданию Java конфигов

Даже в Java конфигах есть много вариантов определения зависимостей между бинами. Рекомендуется делать следующим образом:

1. Не использовать в классах бинов Spring аннотации — вся логика создания и установки зависимостей должна быть в Java конфиге.
2. Конфиги зависят только от других конфигов, бины только от других бинов. Конфиги не наследуем друг от друга — чтобы при автовайринге конфигов была однозначность.
3. Зависимость одного конфига от другого определять с помощью аннотации `@Import` (нужно чтобы каждый конфиг был самодостаточен и мог быть заимпортирован куда угодно без доп условий) и как `final` поле в конфиге (чтобы можно было вызвать `@Bean` методы для связи бинов). Привязка одного конфига к другому по факту будет происходить при помощи autowiring в конструктор. Проблем с autowiring тут нет, так как мы всегда имеем только один инстанс конкретного конфига - конфликтов не может быть.
4. Бины определяются в `@Bean` методах. Если бин должен быть доступен в других конфигах - делаем его public. В противном случае можно делать protected. Для установки зависимостей используются вызовы других `@Bean` методов, как из этого конфига, тик и из других, от которых он зависит. Для этого необходимо, чтобы в `@Bean` методе никогда не было параметров.
6. Имя бина = имя метода. Устанавливать имя в аннотации `@Bean` рекомендуется только если нужно определить один и тот же бин в разных профилях в одном конфиге.
7. В класс бина все зависимости передаются в конструктор. Зависимости устанавливаются в final поля класса.
8. Очень аккуратно использовать component scan. Лучше не использовать вообще, так как это всегда усложняет чтение кода - очень сложно понять, какие все таки бины будут в контексте а каких не будет.
9. Аннотации `@Value` и `@ClasspathResourceValue` используем только в конфигах, как и остальные Spring аннотации. Оставляем в бинах только бизнес логику.

Плюсы данного подхода следующие:

1. Полная защита от циклических зависимостей. Как между бинами так и между конфигами (так как все зависимости через конструктор).
2. Полная детерминированность (при условии запрета на переопределение бинов). Всегда 100% понятно какой именно бин будет использоваться в качестве зависимости.
3. Простота чтения.
4. Навигация и автоподстановка в IDE.
5. Рефакторинг средствами IDE.
6. Простая сборка тестового контекста. Можно использовать целиком конфиги и создавать часть бинов со специфичными для тестов зависимостями.

**Пример конфига с зависимостями**

```java
@Configuration
@Import({
NasConfig.class
})
public class AmazonS3Config {
@Value("${contentlab.mds.s3.endpoint:}")
private String endpoint;

    @Value("${contentlab.mds.s3.access.key:}")
    private String accessKey;

    @Value("${contentlab.mds.s3.secret.key:}")
    private String secretKey;

    @Value("${contentlab.mds.s3.raw.photo.bucket:market-clab-rawphoto}")
    private String rawPhotoBucket;

    @Value("${contentlab.mds.s3.connection.timeout:2000}")
    private int connectionTimeout;

    @Value("${contentlab.mds.s3.read.timeout:60000}")
    private int readTimeout;

    private final NasConfig nasConfig;

    public AmazonS3Config(NasConfig nasConfig) {
        this.nasConfig = nasConfig;
    }

    @Bean
    public AmazonS3 s3Client() {
        BasicAWSCredentials credentials = new BasicAWSCredentials(accessKey, secretKey);
        ClientConfiguration clientConfiguration = new ClientConfiguration();
        clientConfiguration.setConnectionTimeout(connectionTimeout);
        clientConfiguration.setSocketTimeout(readTimeout);

        return AmazonS3ClientBuilder.standard()
            .withCredentials(new AWSStaticCredentialsProvider(credentials))
            .withEndpointConfiguration(new AwsClientBuilder.EndpointConfiguration(endpoint, null))
            .withClientConfiguration(clientConfiguration)
            .withChunkedEncodingDisabled(true)
            .build();
    }

    @Bean
    public AmazonS3Service amazonS3Service() {
        return new AmazonS3Service(
            s3Client(),
            endpoint,
            rawPhotoBucket);
    }

    @Bean
    public RawPhotoS3Service rawPhotoS3Service() {
        return new RawPhotoS3Service(
            amazonS3Service(),
            nasConfig.photoService());
    }
}
```

**Пример класса бина**

```java
public class AmazonS3Service {
private final AmazonS3 s3Client;
private final String endpoint;
private final String bucketName;

    public AmazonS3Service(AmazonS3 s3Client, String endpoint, String bucketName) {
        this.s3Client = s3Client;
        this.endpoint = endpoint;
        this.bucketName = bucketName;
    }
...
}
```

**Пример определения разных бинов в разных окружениях**

```java
@Bean
@Profile("!development")
public StockStorageOutboundClient stockStorageOutboundClient() {
    RequestEntityService requestEntityService =
    new RequestEntityService(createTvmTicketProvider(tvmConfig.tvmClient()));
    return new StockStorageOutboundRestClient(stockStorageRestTemplate(), host, requestEntityService);
}

@Bean("stockStorageOutboundClient")
@Profile("development")
public StockStorageOutboundClient stockStorageOutboundClientDev() {
    RequestEntityService requestEntityService = new DevelopmentRequestEntityService();
    return new StockStorageOutboundRestClient(stockStorageRestTemplate(), host, requestEntityService);
}
```

## Исключения

Из указанных выше правил допустимы исключения, когда можно пользоваться автоинжектом бинов.

- Spring Controller-ы
- Тесты
- Интеграция с чужими конфигами spring
