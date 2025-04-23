## Информация

Библиотека предназначена для тестирования статических и динамических таблиц, подключенных с помощью
библиотеки ```market/adv/adv-shop/yt```.

## Библиотека для тестов

1. ```ru.yandex.market.adv.yt.test.extension.YtExtension``` - класс-расширение для JUNIT 5, нацеленное на
   предварительную загрузку таблиц и их сверку с ожидаемым результатом по завершению выполнения теста.
2. ```ru.yandex.market.adv.yt.test.configuration.YtTestConfiguration``` - конфигурация для тестирования YT.
3. ```ru.yandex.market.adv.yt.test.jackson.deserializer.model.YTreeNodeJsonModel``` - если нам необходимо преобразовать
   элемент json-файла в ```ru.yandex.inside.yt.kosher.ytree.YTreeNode```, то необходимо записать его в файл в виде
   данного класса-модели.

## Тестовые аннотации

1. ```ru.yandex.market.adv.yt.test.annotation.YtUnitDataSet``` - аннотация для описания содержимого YT таблицы.
   Repeatable.
2. ```ru.yandex.market.adv.yt.test.annotation.YtUnitScheme``` - аннотация для описания схемы таблицы YT

## Алгоритм подключения библиотеки

1. Подключить в проект библиотеку ```market/adv/adv-shop/yt``` и настроить ее для тестов по инструкции
   из [README.md](https://a.yandex-team.ru/arc/trunk/arcadia/market/adv/adv-shop/yt#testirovanie-prilozheniya-s-ispolьzovaniem-biblioteki)
2. Для подключения библиотеки достаточно добавить в ```@SpringBootTest```  класс
   конфигурации ```JacksonAutoConfiguration``` и ```YtTestConfiguration``` и
   дописать ```@ExtendWith(YtExtension.class)```.

Пример теста:

```java
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.springframework.boot.autoconfigure.jackson.JacksonAutoConfiguration;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.TestPropertySource;

import ru.yandex.market.adv.config.CommonBeanAutoconfiguration;
import ru.yandex.market.adv.config.YtDynamicClientAutoconfiguration;
import ru.yandex.market.adv.config.YtStaticClientAutoconfiguration;
import ru.yandex.market.adv.test.AbstractTest;
import ru.yandex.market.adv.yt.test.annotation.YtUnitDataSet;
import ru.yandex.market.adv.yt.test.annotation.YtUnitScheme;
import ru.yandex.market.adv.yt.test.configuration.YtTestConfiguration;

@ExtendWith(YtExtension.class)
@SpringBootTest(
    classes = {
        CommonBeanAutoconfiguration.class,
        YtDynamicClientAutoconfiguration.class,
        YtStaticClientAutoconfiguration.class,
        JacksonAutoConfiguration.class,
        YtTestConfiguration.class
    }
)
@TestPropertySource(locations = "/application.properties")
class YtExtensionTest extends AbstractTest {

    @DisplayName("Тест таблиц YT")
    @Test
    @YtUnitDataSet(
        scheme = @YtUnitScheme(
            model = Table.class,
            path = "//tmp/test-table-1322",
            isDynamic = false
        ),
        before = "before.json",
        after = "after.json"
    )
    @YtUnitDataSet(
        scheme = @YtUnitScheme(
            model = AnotherTable.class,
            path = "//tmp/test-table-1323"
        ),
        before = "before.json"
    )
    void ytTableTest_before_after() {
    }

    // ...
}
```
