# Установка и разработка

- Для начала убедитесь, что вы полнили все шаги из [NEWBIE.md](https://a.yandex-team.ru/arc_vcs/taxi/lavka/frontend/docs/NEWBIE.md).

- Добавляем локальные домены в `/etc/hosts`

  ```bash
  echo '127.0.0.1 lavka.local.yandex.ru' | sudo tee -a /etc/hosts
  echo '127.0.0.1 deli.local.yango.com' | sudo tee -a /etc/hosts
  echo '127.0.0.1 10min.local.market.yandex.ru' | sudo tee -a /etc/hosts
  echo '127.0.0.1 deli.local.yango.yandex.com' | sudo tee -a /etc/hosts
  ```

- Заходим в свой аккаунт в [тестовом паспорте](https://passport-test.yandex.ru) (если нет аккаунта, то создать и привязать номер телефона).

- Запускаем приложение

  ```bash
  cd taxi/lavka/frontend
  npm run dev:website
  ```

- Приложение будет доступно на https://lavka.local.yandex.ru


## Локальная сборка

|             |                                      |
| ----------- | ------------------------------------ |
| production  | `npm run build`                      |
| development | `NODE_ENV=development npm run build` |


## Метрика

- Для разработки метрики принято подключать один единственный хук, который пробрасывает все хендлеры метрики
  для страницы и реализует внутри себя необходимые эффекты, выполняемые на странице

События метрики разграничиваются переменной env для разных окружений (production, testing, unstable, development)

- Для отладки метрики добавляем в url параметр: \_ym_debug=1
  [Дока метрики](https://yandex.ru/support/metrica/code/counter-initialize.html)
