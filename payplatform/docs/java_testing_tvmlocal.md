Библиотека tvmlocal
===================

Библиотека позволяет запустить локальный `tvm` для использования тестов - т.е. теперь не требуется рецептов. В данный момент из коробки поддерживаются следующие возможности:

- запуск tvm демона в реальном режиме (с обращением к tvm-api) и в режиме unittest.
- интеграция с micronaut
- запуск на трех основных платформах разработки - Linux, Mac, Windows.

Для начала работы нужно подключить саму библиотеку `payplatform/java/testing/tvmlocal` в `PEERDIR` проекта.

{% note alert %}

Библиотека предназначена исключительно для использования в тестах!

{% endnote %}

Low level API
-------------

`tvmlocal` предоставляет возможность ручного менеджмента и настройки инстансов `tvmtool`. Для этого необходимо запустить `tvmtool`-демон, передав необходимые настройки:

```java
import java.util.OptionalInt;
import ru.yandex.payments.tvmlocal.testing.BinarySandboxSource;
import ru.yandex.payments.tvmlocal.testing.TvmTool;
import ru.yandex.payments.tvmlocal.testing.Utils;
import ru.yandex.payments.tvmlocal.testing.options.ResourceConfigLocation;
import ru.yandex.payments.tvmlocal.testing.options.TvmToolOptions;

class CustomRunner {
    public void run() {
        int port = Utils.selectRandomPort();
        var source = new BinarySandboxSource();
        var configLocation = new ResourceConfigLocation("tvmtool.conf");
        val options = new TvmToolOptions(OptionalInt.of(port), configLocation, Mode.UNITTEST, emptyMap(), TvmToolOptions.generateAuthToken());
        var tool = TvmTool.start(source, options); // запустили tvmtool
        tool.stop(); // остановили tvmtool
    }
}
```

Micronaut-based конфигурация
----------------------------

В случае использования `tvmlocal` в `micronaut`-based тестах достаточно добавить основные настройки в конфиг приложения:

```yaml
tvmlocal:
  mode: unittest # режим работы tvmtool, можно задать любое из значений перечисления Mode
  config: classpath:tvmtool.conf # путь к конфигу tvmtool. префикс 'classpath:' позволяет указать конфиг, хранящийся непосредственно в classpath приложения
```

После этого при старте теста автоматом будет запушен инстанс `tvmtool`. Для подключения будут доступны следующие `properties`:

- `tvmlocal.tvmtool-port` - порт на котором запущен `tvmtool`
- `tvmlocal.tvmtool-auth-token` - токен для подключения к `tvmtool`
