## yplatform::coroutine

Представляет собой вспомогательные классы и функции для stackless корутин. Главная задача - облегчить работу с корутинами, хранящими в себе тяжело копируемые данные.

### yplatform/coroutine.h

`yield_context` - обертка над asio::coroutine.
Передается при вызовах, хранит внутри все данные и саму корутину,
завернутую в shared_ptr.

Пример:
```c++
struct coro
{
  bigdata member1;
  bigdata member2;

  void operator()(yield_context<coro> ctx, boost::system::error_code = {})
  {
    reenter(ctx)
    {
      member1.access();
      yield foo(ctx);
      member2.access();
    }
  }
};
```

`member1` и `member2` не копируются между асинхронными вызовами.

Простой способ получить из асинхронной операции несколько аргументов:
```c++
struct coro
{
  boost::system::error_code ec;
  bigdata data;

  void operator()(yield_context<coro> ctx)
  {
    reenter(ctx)
    {
      yield foo(ctx.capture(ec, data));
      if (!ec) data.access();
    }
  }
};
```

Функция `spawn()` создает и запускает корутину.

```c++
yplatform::spawn(T{bigdata{},bigdata{}});
```

Примеры использования можно найти [тут](../examples/).