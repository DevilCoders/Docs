## Настройки приложений партнёрского интерфейса по умолчанию

Модуль конфигурирует:

* Подключение к `MySql` и создание `@Bean DSLContext`
* Настройку логирования
* Настройку `Spring-actuator`

Чтобы подключить общий конфиг в приложение необходимо добавить зависимость в `ya.make`

        PEERDIR(

            ...

            partner/java/defaultconfiguration
        )

Если нужно использовать свои свойства (properties) или перезаписать свойства по умолчанию через
profile-specific property files, то файлы application-{profile}.yaml нужно располагать в каталоге `resource/config`.

Например для приложения `intapi` файлы с дополнительными свойствами лежат в `arcadia/partner/java/apps/intapi/src/main/resources/config/`

При внесении изменений в конфиги желательно сопровождать их комментариями.

