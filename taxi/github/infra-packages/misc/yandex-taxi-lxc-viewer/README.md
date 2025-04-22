# yandex-taxi-lxc-viewer
Приложение для отображения информации о LXC-контейнерах

**link**: http://lxc-viewer.taxi.yandex.net
**config**: src/models/configuration.py
```
    - /     - основная страница
    - /ping - статус работоспособности сервиса
    - /add_host - endpoint для добавления информации о хостах:

        curl -s -X POST -H "Content-Type: application/json" "http://lxc-viewer.taxi.yandex.net/add_host" -d '[
            {"mac":"",          mac-адрес контейнера
             "name":"",         имя контейнера
             "status":"",       статус контейнера (running/stopped)
             "template":"",     используемый шаблон
             "uuid":"",         uuid-контейнера
             "dom0":"",         имя dom0-хоста, на котором запущен контейнер
             "updated_at":""}   время обновления записи
        ]'
```
