# FAQ

#### **Q: Что делать если нет конфига или он не обновляется?**

**A:** Убедится что хост входит в предикат [работает gfglister] и проверить [статус получения конфига с хоста](https://monitoring.yandex-team.ru/projects/gfglister/dashboards/monmmdu7aokdp3ivb398/view?from=now-1d&to=now&refresh=60000&p.thost=admiral-u2.yndx.net).
Дальше нужно получить подробности через ручку
```shell
 curl -s 'http://gfglister.yandex.net/get_status' | jq -c '.data|to_entries[] | select(.key == "host.yndx.net")'
```
```json
{"key":"m9u-i1013.yndx.net","value":{"lastConfCheck":"2022-07-22T17:47:52.568386859+03:00","lastError":"","lastErrorTime":"0001-01-01T00:00:00Z","lastSuccessfulUpdateTime":"2022-07-22T21:49:29.621055645+03:00","locked":false,"status":1}}
```
В lastError будет описание последней ошибки получения конфига. Если ничего не помогло, то смотрим логи на мастере
```shell
journalctl -S -1h | grep hostname
```

#### **Q: Как получить доступ к конфигам?**

**A:** SVN репозиторий `svn+ssh://arcadia.yandex.ru/robots/trunk/noc/cfglister` администриуется [[тулзами]](https://abc.yandex-team.ru/services/svn/)
и скрыт от чтения обычными пользователями. Для просмотра можно использовать веб морду [WebSVN](https://arc.yandex-team.ru/wsvn/robots/trunk/noc/cfglister/).

Если ссылка на WebSVN не открывается, следует запросить доступ к репозиторию в [st/DEVTOOLSSUPPORT](https://st.yandex-team.ru/DEVTOOLSSUPPORT) ([пример](https://st.yandex-team.ru/DEVTOOLSSUPPORT-5243)).

Возможности смотреть репозиторий через интерфейс a.yandex-team.ru нет, поскольку он не поддерживает разграничение доступа. В cfglister'е хранятся полные конфиги с потенциально чувствительной информацией. a.yandex-team.ru работает с репозиторием с правами общего робота, а WebSVN - с правами пользователя.
#### **Q: Почему так долго разгребает очередь на коммиты?**

**A:** Коммит в SVN может занимать 1-2 секунды, что не является проблемой в обычной жизни.
Если происходит массовая катка, то очередь будет отрастать и это ожидаемое поведение.
Так выглядит разгребание очереди:

[<img src="https://jing.yandex-team.ru/files/gescheit/Screenshot%202022-07-28%20at%2016.26.35.png" width="1000"/>](https://jing.yandex-team.ru/files/gescheit/Screenshot%202022-07-28%20at%2016.26.35.png)
