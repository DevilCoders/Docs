# Аркадийное ядро Jupyter с библиотеками Огорода

1. Собрать ядро

```bash
cd maps/garden/tools/jupyter
ya make -r
```

2. Создать файл `~/.local/share/jupyter/kernels/garden-kernel/kernel.json` со следующим содержимым, подставив имя пользователя:

```json
{
    "argv": [
        "/home/<username>/arc/arcadia/maps/garden/tools/jupyter/jupyter",
        "-m",
        "ipykernel_launcher",
        "-f",
        "{connection_file}"
    ],
    "display_name": "Garden Kernel",
    "language": "python"
}
```

3. Запустить сервер Jupyter:

```bash
/usr/local/bin/jupyter notebook --ip=wicket.sas.yp-c.yandex.net --no-browser
```

На экране будет ссылка, которую можно открыть в браузере: http://wicket.sas.yp-c.yandex.net:8888/?token=1234567890

Если порт 8888 уже занят, то при запуске можно указать другой порт.

Подробнее про аркадийные ядра: https://wiki.yandex-team.ru/jupyter/docs/customarcadiakernel/
