# s2s прокси для WebView Лавки

Прокси сервис на случай блокировок доменов Яндекса.
См. также https://st.yandex-team.ru/LAVKASERVICES-139

---
## production

Боевая сборка живет на Linode хостах, за подробностями нужно идти к администраторам Лавки:
телеграм чат [Lavka-admin](https://t.me/joinchat/AndmkljNdwM1fO7Mh1RDWA),
ответственный администратор [leontyevmax](https://staff.yandex-team.ru/leontyevmax)

GAP проксируется через хост `https://grocery-authproxy.yadeli.org`

Статика проксируется через хост `https://static.yadeli.org`

---
## testing

Тестовый стенд собран во внутренней сети.

GAP проксируется через хост `https://lavka-s2s-proxy.in.yandex.net`

Домен `lavka-s2s-proxy.in.yandex.net` живет в своем Авакс
[неймспейсе](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/testing.lavka-services.s2s/show)

Для этого домена выписан [сертификат](https://crt.yandex-team.ru/certificates/4458396)
(также смотри [секретницу](https://yav.yandex-team.ru/secret/sec-01fxak3vgmqf9hzkd2wvkk29cz/))

Домен указывает на Няня [инстанс в SAS](https://nanny.yandex-team.ru/ui/#/services/catalog/lavka_grocery-superapp_dev-s2s-proxy/)

В android/ios приложении указываем "custom GAP":
`https://lavka-s2s-proxy.in.yandex.net/4.0/grocery-superapp-testing/lavka/`

### Сборка docker контейнера

Команды вызываем из папки `taxi/lavka/frontend/projects/webview/s2s-proxy/testing`

- ssl сертификат
  - качаем сертификат и кладем его в файл `certs/lavka-s2s-proxy.in.yandex.net.pem`
  - приватный ключ кладем в файл `certs/lavka-s2s-proxy.in.yandex.net.key.pem`

- создаем docker конфиг для робота `robot-lavka-infra` (файл `~/.docker/robot-lavka-infra/config.json`)
  ```json
  {
      "auths": {
          "registry.yandex.net": {
              "auth": "<credentials>"
          }
      }
  }
  ```
  где **<credentials>** — это `base64("robot-lavka-infra:secret_token")`

- собираем контейнер
  ```bash
  docker --config ~/.docker/robot-lavka-infra build . --no-cache --pull -t lavka/grocery-superapp/unstable:s2s-proxy
  docker tag lavka/grocery-superapp/unstable:s2s-proxy registry.yandex.net/lavka/grocery-superapp/unstable:s2s-proxy
  docker --config ~/.docker/robot-lavka-infra push registry.yandex.net/lavka/grocery-superapp/unstable:s2s-proxy
  ```

- теперь можно выложить контейнер `lavka/grocery-superapp/unstable:s2s-proxy` через Клоундуктор
