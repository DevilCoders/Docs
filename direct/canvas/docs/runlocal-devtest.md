## Локальный запуск с базой devtest

Часто удобно запустить локально канвас, который бы смотрел в общую монгу, развёрнутую на devtest окружении.
И вызывать его через бету. Это поможет дебажить.

Для этого нужно:

1. Поднять бету с канвасом
    [подробная инструкция](https://st.yandex-team.ru/DIRECTKNOL-32)

    Кратко
    ```
    direct-create-beta --java-svn app:web,app:intapi,app:canvas-backend
    переходим в директорию беты
    beta-ctl prepare canvas
    beta-ctl canvas-enable-frontends-nginx
    beta-ctl start canvas
    ```

    Важно зайти на бету и убедиться что всё работает.

2. Получить TVM секрет с ppcdev. Скорее всего они уже есть.

   `bin/download_secret_for_local_use.py`

   Подробности в https://st.yandex-team.ru/DIRECTKNOL-47

3. Смёрджить аргументы запуска и environ бекенда канваса,
   который бежит на бете, в ENV-переменные для запуска локального канваса.

   Аргументы запуска можно посмотреть через `ps`.
   Пример команды как найти, `ps aux | grep {номер беты} | grep yandex-direct-canvas-backend`
   Проще взять из примера параметры для беты 10530 и заменить на свой номер беты.
   Параметры указать в VM options IDEA.
   ```
   -DVIDEO_ADDITIONS_API_URL=http://127.0.0.32:10530/
   -Dspring.profiles.active=devtest
   -DDIRECT_URL=http://10530.beta3.intapi.direct.yandex.ru
   -DSANDBOX_BASE_URL=https://sandbox.yandex-team.ru/api/v1.0
   -Dbeta.url=http://10530.beta3.direct.yandex.ru
   -DCANVAS_HOST=canvas-10530.beta3.direct.yandex.ru
   -DCANVAS_VA_API_BASE_URL=https://canvas-10530.beta3.direct.yandex.ru/rest/video-additions/
   ```

   Если при запуске `ru.yandex.canvas.Application` возникают проблемы с валидацией серверных сертификатов,
   то стоит посмотреть [инструкцию](https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vjava)
   и добавить параметр trustStore в VM options.
   ```
   -Djavax.net.ssl.trustStore=$JAVA_HOME/lib/security/cacerts
   ```

   ENV-vars можно посмотреть через
   ```
   cat /proc/${process_id}/environ | tr '\0' '\n' | grep -E "SECRET|TOKEN|STRING|KEY|PASSWORD"
   ```
   ${process_id} заменить на нужный номер процесса.
   Пример в документации не привожу, так как там секреты

4. Запустить `ru.yandex.canvas.Application`

    Если нужно пробросить порт с беты локально, можно воспользоваться командой
    ```
    kill 385429 # убить процесс беты. Номер процесса узнали из предыдущего пункта
    beta-ctl use-canvas-from-ssh-tunnel #на бете
    ssh -R 127.0.0.40:10530:localhost:8080 ppcdev3 #локально. С ноутбука. Номер беты 10530 и ppcdev может отличаться
    ```
    Обратите внимание, что команда `beta-ctl use-canvas-from-ssh-tunnel` выдаст что-то вроде этого:
    ```
    # команда для поднятия ssh-тоннеля выполнять на локальной машине (рабочем ноутбуке)
    ssh -R 127.0.0.40:10530:localhost:8090 ppcdev3
    # сбросить командой
    beta-ctl unset java_canvas_endpoint
    ```
    Но ваш локальный канвас, вероятно, запустился на другом порту - 8080.
    Точно узнать порт можно в консоли Idea, там будет строчка похожая на эту:
    ```
    2020-11-03:15:09:35.581076 [main] INFO  org.springframework.boot.web.embedded.jetty.JettyServletWebServerFactory - Server initialized with port: 8080
    ```
