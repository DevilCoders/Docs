# Образ Opera

Здесь и далее `<version>` - это необходимая версия браузера, доступная во внешнем репозитории `docker.io/selenoid/opera:<version>`.

Собрать образ:
```bash
$ BROWSER_VERSION=<version>; docker build --build-arg BROWSER_VERSION=$BROWSER_VERSION -t registry.yandex.net/selenium/opera:$BROWSER_VERSION .
```

Запустить образ:
```bash
$ BROWSER_VERSION=<version>; docker run -it --rm --privileged -p 4444:4444 -p 5900:5900 -e ENABLE_VNC='true' registry.yandex.net/selenium/opera:$BROWSER_VERSION
```

Проверить образ:
  - поднять сессию:
    ```bash
    $ BROWSER_VERSION=<version>; curl --header "Content-Type: application/json" -v http://127.0.0.1:4444/session -d '{"capabilities":{"alwaysMatch":{"browserName":"opera","browserVersion":"'"$BROWSER_VERSION"'"}},"desiredCapabilities":{"browserName":"opera","browserVersion":"'"$BROWSER_VERSION"'"}}'
    ```
  - открыть VNC:
    ```bash
    vnc://127.0.0.1:5900 # пароль 'selenoid'
    ```

Запушить образ:
```bash
$ BROWSER_VERSION=<version>; docker push registry.yandex.net/selenium/opera:$BROWSER_VERSION
```
