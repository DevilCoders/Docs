# Мониторинг квоты

Чтобы своевременно получать уведомления о превышении порогов использования квоты для своих ключей API можно настроить алерт в Головане и проверку в Juggler.

Сигналы можно посмотреть на панели <https://yasm.yandex-team.ru/template/panel/maps_core_renderer_staticapi-ratelimiter2-panel>

Алерт настраивается для следующего сигнала (`<YOUR_API_KEY>` нужно заменить на свой ключ API):

```
signals=
    or(
        na(
            perc(
                yacare-ratelimiter-server_<YOUR_API_KEY>@maps_core_renderer_staticapi_dxxm,
                sum(
                    yacare-ratelimiter-server_<YOUR_API_KEY>@maps_core_renderer_staticapi_dxxm,
                    yacare-ratelimiter-server_<YOUR_API_KEY>@maps_core_renderer_staticapi_quota_dnnm
                )
            )
        ),
        0
    );
hosts=ASEARCH;
itype=maps;
ctype=prestable, stable
```

Пример алерта: <https://yasm.yandex-team.ru/alert/maps_core_renderer_staticapi_quota_stable.anonym>

Пример шаблона алертов для квоты:
- <https://yasm.yandex-team.ru/template/alert/maps_core_renderer_staticapi_quota_stable>
- <https://a.yandex-team.ru/arc_vcs/maps/renderer/staticapi/quota_alerts>
