# Конфигурирование окружения

Для подключения библиотеки нужно импортировать в приложение класс [CommonEnvConfiguration](src/main/java/ru/yandex/market/wms/shared/libs/env/conifg/CommonEnvConfiguration.java):
```
@Import(
    CommonEnvConfiguration.class,
    ...
)
class JavaApp {
```
```
@Import(
    CommonEnvConfiguration::class,
    ...
)
class KotlinApp {
```

