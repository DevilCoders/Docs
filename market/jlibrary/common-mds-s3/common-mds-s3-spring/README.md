
# Spring конфигурации

Для того чтобы добавить библиотеку в Spring-based проект, заготовлены специальные конфигурации.


## MdsS3BasicConfiguration

Базовая конфигурация для интеграции с MDS S3.

Предоставляет следующие бины:
- `AmazonS3` - клиент для работы с Amazon S3 из [aws-java-sdk-s3](https://github.com/aws/aws-sdk-java/tree/master/aws-java-sdk-s3)
- `MdsS3Client` - более высокоуровневый клиент для работы с S3, работающий с `ResourceLocation`, `ContentProvider` & `ContentConsumer`

Для использования конфигурации необходимы параметры:
- `market.mds.s3.access.key` - ключ доступа
- `market.mds.s3.secret.key` - секретный ключ
- `market.mds.s3.path` - endpoint, присутствует по умолчанию в datasources

Для переопределения параметров, можно использовать placeholder'ы:
```properties
market.mds.s3.access.key = ${mbi.mds.s3.access.key.id}
market.mds.s3.secret.key = ${mbi.mds.s3.secret.key.id}
```

Так же можно использовать соответствующие getter-методы, унаследовав конфигурацию, ex:
```java
@Configuration
public static class OverrideConfig extends MdsS3BasicConfiguration {
    @Value("${access.key}") String accessKey;
    @Value("${secret.key}") String secretKey;
    @Value("${endpoint}") String endpoint;

    @Override protected String getAccessKey() { return accessKey; }
    @Override protected String getSecretKey() { return secretKey; }
    @Override protected String getEndpoint() { return endpoint; }
}
```


## MdsS3LocationConfiguration

Данная конфигурация удобна в том случае, если вам необходимо работать (в основном) с одним bucket'ом.
Регистрирует бин `ResourceLocationFactory`, который будет создавать `ResourceLocation`'ы с указаным bucket'ом.

Обязательные параметры:
- `market.mds.s3.default.bucket.name` - наименования bucket'a в S3

Опциональные параметры:
- `"market.mds.s3.default.path.prefix"` - префикс для всех локаций, созданных через фабрику


## MdsS3HistoryConfiguration

`ResourceConfiguration` - это более высокоуровневые выгрузки:
- Пути до файлов и их имена всегда в заданном формате (см `KeyGenerator`)
- Есть возможность указывать TTL (`ResourceLifeTime`)
- Можно настраивать ведение исторических данных (см. `ResourceHistoryStrategy`)

Конфигурация предоставляет базовые бины для работы с `ResourceConfiguration`:
- `KeyGenerator` - генератор S3-ключей (путь до файла в терминах S3)
- `PureHistoryMdsS3Client` - клиент для работы с `ResourceConfiguration`


## MdsS3ResourceConfiguration

Все конфигурации ресурсов регистрируются в реестре / провайдере и к ним можно обращаться по имени.

Предоставляет следующие бины:
- `ResourceConfigurationFactory` - фабрика для создания конфигураций ресурсов
- `ResourceConfigurationProvider` - реестр / провайдер `ResourceConfiguration`
- `NamedHistoryMdsS3Client` - клиент для работы с `ResourceConfiguration`, использующий их имена

Обязательные параметры:
- `market.mds.s3.default.bucket.name` - наименования bucket'a в S3


## MdsS3ValidatorConfiguration

Эта конфигурация создает и запускает `ResourceConfigurationValidator`, который проверяет все доступные конфигурации из `ResourceConfigurationProvider`.
Может быть использован для стандартизации наименований директорий и файлов.


## MdsS3CleanerConfiguration

Конфигурация позволяет отслеживать и зачищать / удалять старые конфигурации ресурсов.

Для использования конфигурации необходимы параметры:
- `servant.name` - имя приложения, которое регистрирует `ResourceConfiguration`
- `market.mds.s3.configuration.table` - таблица БД, в которую будут храниться данные о `ResourceConfiguration`

Предоставляет следующие бины:
- `ResourceConfigurationDao` - DAO для работы с конфигурациями ресурсов
- `MdsS3ResourceConfigurationDetector` - компонент для сохранения найденных в приложении конфигураций ресурсов в БД, запускается при старте контекста Spring
- `MdsS3ResourceConfigurationCleaner` - компонент для зачистки / удаления старых конфигураций ресурсов

Можно также посмотреть common-mds-s3-tms, который предоставляет готовые TMS-задачи, в том числе по зачистке.
