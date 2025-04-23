## Модули

### Определение модуля
Модуль - это класс, отнаследованный от `yplatform::module`.

Минимальный пример модуля:

```c++
#include <yplatform/module.h>
struct module: yplatform::module
{};
```

У модуля есть имя и логгер:

```c++
struct module: yplatform::module
{
  void greeting()
  {
    YLOG(logger(), info) << "Hello!";
    YLOG_L(info) << "My name is " << name();
  }
};
```
Также модуль наследуется от `std::enable_shared_from_this<yplatform::module>`. Это позволяет управлять его временем
жизни. Важно помнить, что функция `shared_from_this()` вернет указатель на
`yplatform::module`. Чтобы получить указатель на конкретный класс модуля, используйте
`yplatform::shared_from()`:

```c++
auto self = yplatform::shared_from(this);
```

### Модули под управлением платформы
#### Создание и регистрация
Платформа умеет при старте приложения создавать модули по конфигу.

Создайте класс модуля и зарегистрируйте его следующим образом:

```c++
#include <yplatform/module_registration.h>
REGISTER_MODULE(yhttp::call_impl)
```

Объявите модули в конфиге приложения:

```yaml
modules:
  module:
  - _name: http_client
    system:
      name: http_client
      factory: yhttp::call_impl
    configuration:
      reuse_connection: on
```

При инстанцировании модуля платформа выберет первый подходящий конструктор по следующему списку приоритетов:

```c++
module(yplatform::reactor_set&, const yplatform::ptree& configuration);
module(yplatform::reactor&, const yplatform::ptree& configuration);
module(io_service&, const yplatform::ptree& configuration);
module(yplatform::reactor_set&);
module(yplatform::reactor&);
module(io_service&);
module(const yplatform::ptree& configuration);
module();
```

#### Жизненный цикл модуля
Опционально определите следующие методы:
```c++
void init();
void init(const yplatform::ptree& configuration);
void start();
void reload(const yplatform::ptree& configuration);
void stop();
void fini(); // deprecated
```
- `init()` - используется как замена конструктору, когда необходим доступ в логгеру или shared_from_this
- `start()` - модуль запускает все фоновые процессы, начинает принимать входящую нагрузку
- `reload()` - перечитать конфиг
- `stop()` - закрыть порты, остановить фоновую активность
- `fini()` - вызывает после остановки I/O реакторов

См. также [жизненный цикл приложения](lifecycle.md).

#### Поиск модулей
Во время инициализации, приложение регистрирует модули в глобальном репозитории.
После этого к ним можно обращаться с помощью функции yplatform::find:

```c++
#include <yplatform/find.h>
...
auto http_client = yplatform::find<yhttp::client>("http_client");
```

По соображениям обратной совместимости используется boost::shared_ptr.

### Использование модулей без платформы
Модули можно создавать и использовать вне платформы. В этом случае глобальные репозитории не будут
проинициализированы. Вместо этого сохраните сервисы логов, репозитории контекстов и модулей внутри `boost::asio::io_service`:

```c++
#include <yplatform/app_service.h>
#include <yplatform/module.h>

struct module: yplatform::module
{};

int main() {
  boost::asio::io_service io;
  // init local log service
  yplatform::log::init_console(io);
  // get logger
  auto logger = yplatform::log::find(io, "global");
  {
    auto module = std::make_shared<module>();
    // register in local repository
    yplatform::register_module(io, "name", module);
  }
  // find module
  auto module = yplatform::find<yhttp::client>(io, "name");
}
```
