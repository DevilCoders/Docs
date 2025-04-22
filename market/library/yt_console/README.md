# Описание
Библиотека содержит в себе общую часть бинарников, которые работают с YT и консольными опциями.

Обратите внимание, что заголовочный файл содержит все часто используемые инклуды.

В поддиректории содержится шаблон такого проекта, его достаточно скопировать и начать писать свой код.

## RUN_YT_MAIN
Макрос, убирает копипасту из main функции, инициализирует YT, парсит консольные опции и запускает вашу функцию.

Нужно передать функцию с сигнатурой int(const TOptions& options).

## TYtParameters -- yt proto options
Позволяет добавить часто используемые параметры для работы с YT в консольную программу.

В протобуф опций нужно добавить:

```
import "market/library/yt_console/proto/yt_options.proto";
...
required NMarket.NYTHelper.TYtParameters Yt = 1;
```

И автоматически появятся опции:

```
  --yt-proxy <name>      [Required] YT cluster to use
  --yt-proxy-role <proxy_role>
                         [Optional] Proxy role for YT table reader
  --yt-token-path <path> [Optional] Path to the file containing YT's OAuth token
  --yt-pool <string>     [Optional] YT pool to run all operations in
  --yt-client-log-path <path>
                         [Optional] Path to the YT client log
```

Чтобы создать YT клиента, не нужно проверять эти параметры вручную, достаточно
написать в своей программе:

```
auto yt = NMarket::NYTHelper::CreateYtClient(options.GetYt());
```

[Пример использования](https://a.yandex-team.ru/arc_vcs/commit/r8264838)
