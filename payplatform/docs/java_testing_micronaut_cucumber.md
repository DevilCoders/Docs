Библиотека micronaut-cucumber
=============================

Данная библиотека представляет собой модуль интеграции `micronaut` и `cucumber`. Данный модуль обеспечивает запуск `micronaut` тестов на базе `junit 4`, т.к. из коробки `micronaut` поддерживает интеграцию только с `junit 5`, а `cucumber` расширяет `junit 4`. На данный момент модуль предоставляет:

- Запуск `micronaut` тестов при помощи junit4 runner'a `cucumber`.
- Поддержка `micronaut DI` в `cucumber`.
- Поддержка моков бинов в скоупе тестового класса.
- Возможность запуска нескольких тестов с разной конфигурацией (по сути можно запускать несколько тестовых классов, аннотированных `@MicronautTest`, с произвольным набором `*.feature` файлов).

{% note warning %}

Тесты запускаются при помощи `junit5 vintage-engine`, из-за чего фичи `junit 5` (расширения, хуки и т.д.) не поддерживаются.

{% endnote %}

{% note warning %}

Параллельный запуск тестов не поддерживается ввиду особенностей устройства cucumber.

{% endnote %}

Использование
-------------

Для использования модуля необходимо подключить его в качестве зависимости в ya.make теста и настроить annotation processors.

```yamake
INCLUDE(${ARCADIA_ROOT}/payplatform/java/test.inc) # подключаем общие зависимости и параметры сборки

PEERDIR(
    payplatform/java/testing/micronaut_cucumber
)

# настраиваем annotation processors
ANNOTATION_PROCESSOR(
    io.micronaut.annotation.processing.TypeElementVisitorProcessor
    io.micronaut.annotation.processing.AggregatingTypeElementVisitorProcessor
    io.micronaut.annotation.processing.PackageConfigurationInjectProcessor
    io.micronaut.annotation.processing.BeanDefinitionInjectProcessor
    io.micronaut.annotation.processing.ServiceDescriptionProcessor
)
```

Далее необходимо описать классы тестов, каждый из которых будет использовать независимый DI-контекст.

```java
import io.cucumber.junit.Cucumber;
import io.cucumber.junit.CucumberOptions;
import io.micronaut.test.annotation.MicronautTest;
import org.junit.BeforeClass;
import org.junit.RunWith;
import ru.yandex.payments.testing.micronaut_cucumber.MicronautCucumberTest;

@MicronautTest // Подключаем micronaut, все фичи (установка свойств, настройка окружения и т.д.) тестового фреймворка поддерживаются
@RunWith(Cucumber.class) // Указываем, что тест будет запущен cucumber'ом
@CucumberOptions( // Настраиваем cucumber
    features = "classpath:scenarios.feature", // выбираем feature-файлы, которые будут запущены в данном тесте
    extra_glue = MicronautCucumberTest.EXTRA_GLUE // указываем package, т.к. по-умолчанию cucumber ищет хуки и степы в package теста
)
class MyTest extends MicronautCucumberTest {
    @BeforeClass // обязательно используем аннотацию из junit4
    public static void init() {
        init(MyTest.class); // для корректной инициализации необходимо передать класс теста
    }
}
```

Примечание
----------

Библиотека не претендует на звание general purpose решения, т.к. интеграция собрана из соломы и палок путем эмуляции `extension context` из `junit 5` на базе средств, имеющихся в `junit 4` и `cucumber`.
Возможно некоторые фичи тестового фреймворка `micronaut` не будут работать и потребуют дальнейшей шлифовки напильником.
Лучшим решением будет дождаться нормальной интеграции `cucumber` с `junit 5` (текущая интеграция недокументированна и сильно ограничена в возможностях).
