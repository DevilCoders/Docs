## Библиотека для тестов

1. ```ru.yandex.market.adv.test.AbstractMockServerTest``` - общий наследник для всех тестовых классов, в которых
   требуется поднятие mock сервиса для отправки http запросов.
2. ```ru.yandex.market.adv.test.AbstractTest``` - общий наследник для всех тестовых классов. Нужен, чтобы честно
   инициализировать контекст приложения в тестах.

## Как правильно написать тест

Создать абстрактного наследника от одного из заданных классов и прописать в нем параметры **spring-boot-test**.
Например:

```java

import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.TestPropertySource;

import ru.yandex.cms.client.mock.CmsMockClientConfig;
import ru.yandex.market.adv.config.EmbeddedPostgresAutoconfiguration;
import ru.yandex.market.adv.test.AbstractTest;
import ru.yandex.market.javaframework.main.config.SpringApplicationConfig;
import ru.yandex.market.mboc.common.utils.PGaaSZonkyInitializer;

@SpringBootTest(
    webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT,
    classes = {
        EmbeddedPostgresAutoconfiguration.class,
        SpringApplicationConfig.class,
        CmsMockClientConfig.class
    }
)
@ContextConfiguration(initializers = PGaaSZonkyInitializer.class)
@TestPropertySource(locations = "/99_functional_application.properties")
public abstract class AbstractContentManagerTest extends AbstractTest {
}
```
