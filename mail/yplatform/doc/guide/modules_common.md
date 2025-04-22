## Создание модуля

Модуль - это класс-наследник `yplatform::module`.

Чтобы написать свой модуль, достаточно такого кода:

```c++
#include <yplatform/module.h>

struct module: yplatform::module
{
};
```

Обычно модуль все же имеет настройки и использует какой-то реактор. Поэтому конструктор вашего модуля скорее будет одним из:

```c++
module(yplatform::reactor&, const yplatform::ptree& configuration);
module(yplatform::reactor&);
module(const yplatform::ptree& configuration);
```

Чтобы загрузчик смог найти конструктор для модуля, зарегистрируйте модуль с помощью макроса `REGISTER_MODULE()`.

Рекомендуется также для модуля завести отдельную структуру с настройками и в конструкторе парсить  `ptree` в эту структуру.

Таким образом, шаблон модуля выглядит так:

```c++
#include <yplatform/module.h>

struct settings
{
};

class module: public yplatform::module
{
public:
    module(yplatform::reactor& reactor, const yplatform::ptree& configuration);

private:
    settings settings_;
};

#include <yplatform/module_registration.h>
REGISTER_MODULE(module)
```

Для тестирования или локального создания модулей можно дополнительно объявить конструктор, принимающий  `settings` параметром вместо `ptree`.

## Конфигурация

Конфиг передается в конструктор или `init()` как объект класса `ptree`. Разбор параметров происходит примерно так:
```c++
struct settings
{
    size_t max_size = 4096;
    bool enable_feature_x = false;
  
    settings(const ptree& config)
    {
        max_size = config.get("max_size", max_size);
        enable_feature_x = config.get("feature_x", enable_feature_x);
    }
};
```

Данный пример иллюстрирует следующую рекомендацию: задавайте дефолтные значения в структуре настроек и передавайте параметром в `ptree::get()`. Это выведет шаблонный тип для `ptree::get()` и позволит не дублировать дефолты.

Для `bool` определены конвертеры, допускающие различные форматы записи:

- on/off
- 1/0
- true/false
- yes/no

Прочитать из `ptree` коллекцию элементов в массив или множество можно вспомогательной функцией `read_ptree_to_collection()` из `yplatform/ptree.h` .

### Функции управления модулем

Опционально определите следующие методы:

- `init()` - используется как замена конструктору, когда необходим доступ в логгеру или `shared_from_this`

```c++
void init();
void init(const yplatform::ptree& configuration);
```

- `start()` - модуль запускает все фоновые процессы, начинает принимать входящую нагрузку

```c++
void start();
```

- `reload()` - перечитать конфиг

```c++
void reload(const yplatform::ptree& configuration);
```

- `stop()` - вызывается, чтобы закрыть порты и остановить фоновую активность

```c++
void stop();
```


- `fini()` - вызывается после остановки I/O реакторов, используется редко

```c++
void fini();
```

Эти методы вызывает загрузчик - см. [жизненный цикл приложения](lifecycle.md).

## Дополнительные сведения

### shared_from_this

Часто асинхронный код требует управления временем жизни модуля, поэтому базовый класс модуля наследуется от `enable_shared_from_this<yplatform::module>`.

Получить указатель на конкретный класс модуля можно с помощью функции `yplatform::shared_from()`:

```c++
auto self = yplatform::shared_from(this);
```

### Файловая структура

По возможности разделяйте интерфейс модуля и его реализацию. Это уменьшает связность и время компиляции проектов, улучшает тестируемость кода.

Типовой проект для переиспользуемого модуля выглядит так:

```
module/
  include/
    module/
      module.h
      settings.h
  src/
    impl.h
    impl.cc
    settings.cc
```

Для модулей внутри конечного сервиса такая структура не нужна, размещайте исходники в соответствии со структурой проекта.