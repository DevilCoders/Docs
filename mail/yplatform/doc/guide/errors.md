## Обработка ошибок

### Коды ошибок

Для обработки ошибок в асинхронном коде обычно используются коды ошибок. В платформе распространено использование `boost::system::error_code`.

#### Пример

Объявление перечисления для ошибок HTTP клиента:

```c++
enum class http_error {
    success = 0,
    connect_error,
    ssl_error
};

struct http_error_category : boost::system::error_category {
    const char* name() const noexcept
    {
        return "http_error_category";
    }

    string message(int e) const
    {
        switch (static_cast<http_error>(e)) {
        case http_error::success:
            return "success";
        case http_error::connect_error:
            return "connect error";
        case http_error::ssl_error:
            return "ssl error";
        }
    }

    static const http_error_category& instance()
    {
        static http_error_category category;
        return category;
    }
};

boost::system::error_code make_error_code(http_error e)
{
    return boost::system::error_code(static_cast<int>(e), http_error_category::instance());
}

namespace boost::system {

template <>
struct is_error_code_enum<http_error>
{
    static const bool value = true;
};

}
```

Использование в коде приложения:

```c++
boost::system::error_code err = http_error::connect_error;
if (err) {
    std::cout << "error: " << err.message() << std::endl;
}
```

Вывод: `error: connect error`.

### Пользовательские сообщения об ошибках

Если кода недостаточно и хочется иметь больше диагностической информации, можно воспользоваться классом `yplatform::error`. Он содержит код и дополнительное текстовое сообщение.

#### Пример

Рассмотрим использование `yplatform::error` на том же примере с `http_error`. Определения `enum class http_error` и `struct http_error_category` остаются прежними, к ним добавляется функция `error_category` и специализация шаблона для `yplattform::is_error_enum`:

```c++
const boost::system::error_category& error_category(http_error)
{
    return http_error_category::instance();
}

namespace yplatform {

template <>
struct is_error_enum<http_error>
{
    static const bool value = true;
};

}
```

Использование в коде приложения:

```c++
yplatform::error err(http_error::ssl_error, "expired certificate");
if (err) {
    std::cout << "error: " << err.message() << std::endl;
}
```

Вывод: `error: ssl error: expired certificate`.
