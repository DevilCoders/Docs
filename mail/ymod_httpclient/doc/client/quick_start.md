## Быстрый старт
```C++
yhttp::client httpclient;
auto request = yhttp::request::GET("https://push.yandex.ru/ping");
auto task_context = boost::make_shared<yplatform::task_context>();
httpclient.async_run(task_context, request,
  [](const boost::system::error_code& ec, yhttp::response response) {
    cout << ec.message() << " " << response.status << endl;
  });
```

