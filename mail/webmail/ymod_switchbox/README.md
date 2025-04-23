# Что
Модуль для работы с булевскими значениями в рантайме

# Зачем
Одним из примеров использования является изменение конфига в рантайме. На данный момент модуль сохраняет значение и имеет возможность изменять его либо вызовом ручек, либо через слежение за наличием заданного файла. Конкретным примером такого использования является включение/выключение тыквы в сервисах.

# Как устроено
На данный момент поддержаны следующие стратегии использования:
1) ```http```
2) ```file```

```http``` стратегия предоставляет ручки для каждого значения с путем ```{path}``` из конфигурации:
* POST ```/ymod_switchbox/{path}/enable```
* POST ```/ymod_switchbox/{path}/disable```

```file``` стратегия предоставляет наблюдатель за файлом с путем ```{path}``` из конфигурации.

**По умолчанию** на старте все стратегии имеют значение ```false```.

Также модуль предоставляет ручку GET ```/ymod_switchbox/status```, которая возвращает в поле ```values``` словарь всех значений из модуля.

Интерфейс модуля:
```cpp
using OnValue = io_result::Hook<bool>;

struct ModuleProvider {
    virtual ~ModuleProvider() = default;

    template<class Handler>
    auto waitExpectedValue(const std::string& name, bool expectedValue, Handler handler) {
        io_result::detail::init_async_result<Handler, OnValue> init(handler);
        asyncWaitExpectedValue(name, expectedValue, init.handler);
        return init.result.get();
    }

    virtual bool getValue(const std::string& name) = 0;

protected:
    virtual void asyncWaitExpectedValue(const std::string& name, bool expectedValue, OnValue hook) = 0;
};
using ModuleProviderPtr = std::shared_ptr<ModuleProvider>;
};
```

Метод ```getValue``` возвращает булевское значение для переменной с именем ```name```.  Значение возвращается по принципу побитового ```or``` от всех стратегий для заданного значения. Если метод вызывается с именем переменной, которого нет в конфигурационном файле, то будет вызвано исключение, т.к все переменные известны заранее и вызов несуществующего значения - это проблема программиста.
Метод ```waitExpectedValue``` предоставляет вызывающей стороне реализацию 'ожидателя' конкретного значения для продолжения выполнения, пример вызова можно посмотреть [тут](https://a.yandex-team.ru/svn/trunk/arcadia/mail/webmail/ymod_switchbox/example/module.cc?rev=r9754418#L43). В качестве результата хук возвращает булевское значение аргумента ```expectedValue``` из метода.

# Конфигурирование
Пример конфигурации:
```yaml
-   _name: switchbox
        system:
            name: switchbox
            factory: ymod_switchbox::FileAndHttp
        configuration:
            file_read_timeout: 1s
            inspect_timeout: 1s
            dependencies:
                server: web_server
                reactor: global
                logger: example
            handlers:
            -   strategy: http
                name: module_ready
                path: module/ready
            -   strategy: file
                name: module_ready
                path: /var/tmp/module_ready.txt
    -   _name: worker
        system:
            name: worker
            factory: switchbox_example::Worker
        configuration:
            dependencies:
                reactor: worker_reactor
                switchbox: switchbox
```

## Секция `configuration`
```file_read_timeout``` - опциональный параметр. Обязателен при использовании ```file``` стратегии, представляет собой таймаут между проверками файла.

```inspect_timeout``` - обязательный параметр. Представляет собой таймаут между проверками значения в методе ```waitExpectedValue```.

Узел `dependencies` содержит зависимости модуля:
* `dependencies.reactor` - обязательная зависимость. Реактор нужен для ручек, а также таймеров при слежении за файлом и метода ```waitExpectedValue```.
* `dependencies.server` - обязательная зависимость. Web_server для ручек модуля.
* `dependencies.logger` - обязательная зависимость. Логгер модуля. 

Узел `handlers` содержит список стратегий модуля, каждая стратегия представляет собой следующий список параметров:
* ```strategy``` - строковое представление стратегии (на данный момент ```http```/```file```)
* ```name``` -  имя переменной, по которому можно обращаться в методах модуля
* ```path``` - путь для хранения значения, для каждой стратегии имеет свое определение, примеры подставления данного параметра в ```url```, либо в файловый путь описывались ранее

# Примеры
Лежат в папке [example](https://a.yandex-team.ru/svn/trunk/arcadia/mail/webmail/ymod_switchbox/example)
