В корне проект можно положить файл .env с базовыми переменными среды следующего содержание
```sh

HOST=gradient.local.yandex-team.ru
DEVSERVER_PORT=8080

HTTPS=true
SSL_KEY_FILE=/tmp/certs/gradient.local.yandex-team.ru.key
SSL_CRT_FILE=/tmp/certs/gradient.local.yandex-team.ru.crt
```

# Переменные окружения
* **DEVSERVER_PORT** — порт на котором запуститься дев-сервер
* **HOST** — хост для поднятия  дев-сервера
* **SSL_KEY_FILE** — путь к файлу ключа сертификата (генерируется командой `npm run update-dev-crt`. См. [Readme.md](../Readme.md))
* **SSL_CRT_FILE** — путь к файлу сертификата
* **WITH_RUM** — включение отправки RUM-счётчиков при локальной разработке
* **WITH_MOOA** — включение жука при локальной разработке
* **WITH_METRICA** — включение отправки данных метрики при локальной разработке
* **METRICA_CONFIG** — задание параметров для метрики в формате `webvisor:clickmap:trackLinks:accurateTrackBounce` \
  Например, `1:0:1` — _webvisor_ - включен, _clickmap_ — выключен, _trackLinks_ — включен, _accurateTrackBounce_ - включен по умолчанию \
  Значение по умолчанию — `0:1:1:1`
* **DEBUG** — вывод отладочной информации в консоль сервера
  compile-swagger | baseapi
