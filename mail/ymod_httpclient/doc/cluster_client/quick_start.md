## Быстрый старт

```C++
boost::asio::io_service io;
yhttp::cluster_client::settings st;
st.nodes = { "httpstat.us/500", "httpstat.us/200" };
st.retry_policy.max_attempts = 2;
st.retry_policy.codes = {500};
yhttp::cluster_client client(io, st);

auto ctx = boost::make_shared<yplatform::task_context>();
client.async_run(ctx, yhttp::request::GET("/"), [](auto&& ec, auto&& response) {
    cout << ec.message() << " " << response.status << endl;
});
io.run_for(std::chrono::seconds(2));
```

