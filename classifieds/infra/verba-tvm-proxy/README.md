# verba-tvm-proxy

Сервис для подмешивание в заголовки HTTP запросов к BlackBox TVM токена.

Нужен для перевода legacy проекта verba на походы через TVM.

Тикет: [VERTISADMIN-26746](https://st.yandex-team.ru/VERTISADMIN-26746)

### ТЗ

> Нужен не прокси, а сервер сбоку который будет прикидываться bb, подмешивая tvm
>
> Отдельно стоящий сервис Игорь не одобрил.
>
> Селим сервис в контейнер, xscript натравливаем на него кк на bb
> blackbox.yandex-team.ru:443/blackbox
>
> В хедеры мы кладём
> 'X-Ya-Service-Ticket': {tvmTicket},
> 'content-type': 'application/json',
>
> А дальше просто в query GET-запроса либо в body POST-запроса (можно так и так, будет одинаково) тупо отправлять всё, что прилетает от XScript-а в POST-запросе в body.
> Ну за исключение dbfields может

### config

```go
type config struct {
    BlackboxTvmID int    `env:"VRB_BLACKBOX_TVM_ID" envDefault:"223"`
	BlackBoxURL   string `env:"VRB_BB_UPSTREAM" envDefault:"https://blackbox.yandex-team.ru/blackbox"`
	DeployGTvmID  int    `env:"_DEPLOY_G_TVM_ID"`
	ListenPort    int    `env:"VRB_LISTEN_PORT" envDefault:"8848"`
	QloudTvmToken string `env:"QLOUD_TVM_TOKEN"`
	TraceEnabled  bool   `env:"VRB_TRACE" envDefault:"False"`
	TvmToolPort   int    `env:"VRB_TVMTOOL_PORT" envDefault:"8849"`
}
```
