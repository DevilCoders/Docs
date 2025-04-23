#  Работа с секретами

Секреты будут автоматически созданы и добавлены как переменные окружения при деплое.

Подробнее [auto#sekrety](../auto.md#sekrety)

{% cut "Ручная работа с секретами" %}

**Для доставки секретов в деплой нужно:**
- добавить секрет в [секретницу](https://yav.yandex-team.ru)
- делегировать секрет через cli-утилиту (см. [пример использования](#delegirovanie-sekreta))
- Вписать в [манифест деплоя](../service-preparation/manifest.md) env вида `SECRET_VAR: '${sec-01dkem0gfttbqd677hvyj42r2h:ver-01djnj5xyrc4xsr4wjmrfyrw5e:somekey}'`

##  Важные особенности
- Делегировать секрет можно только при наличии [карты сервисов](../service-map.md).
- Если значение секрета было загружено как файл, оно придёт в переменные окружения как значение в base64

##  cli-утилита
- Установка для OSX:
```(bash nomark)
brew tap YandexClassifieds/vertis ssh://git@bb.yandex-team.ru/yandex-classifieds/homebrew-vertis.git
brew update
brew install yandexclassifieds/vertis/sscli
```
- Установка для Linux:
```(bash nomark)
sudo curl https://s3.mds.yandex.net/vertis-share/sscli/sscli-linux-0.6.0 -o /usr/local/bin/sscli && sudo chmod +x /usr/local/bin/sscli
```
- OAuth-токен брать [здесь](http://oauth.yandex-team.ru/authorize?response_type=token&client_id=f33f3a3b3fbe4f28a870ac070d60e681)
- Добавить токен в переменные окружения:
```(bash nomark)
echo export VSS_OAUTH_TOKEN="<YOUR_TOKEN>" >> ~/.bashrc
source ~/.bashrc
```
- Посмотреть/создать нужный секрет в [Яндекс.Секретнице](https://yav.yandex-team.ru)

## Пример использования
### Делегирование секрета
```
$ sscli delegate --secret-id sec-01dkem0gfttbqd677hvyj42r2h grpc-echo
secret sec-01dkem0gfttbqd677hvyj42r2h was added for service 'grpc-echo'
```
### Отмена делегирования
```
$ sscli revoke grpc-echo -s sec-01dkem0gfttbqd677hvyj42r2h
2021/07/23 16:38:23 revoked token: tid-01fb9pdxrkcj1ynhzsvyqwc1pn
```

{% endcut %}
