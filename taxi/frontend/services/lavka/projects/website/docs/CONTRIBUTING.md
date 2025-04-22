## Установка и разработка

Для работы с проектом потребуются

- [nvm](https://github.com/nvm-sh/nvm)
- node и npm

Чтобы запустить проект локально

- Клонируем репозиторий и переходим в директорию с проектом

  ```bash
  git clone git@github.yandex-team.ru:taxi/frontend-monorepo.git
  cd frontend-monorepo/services/lavka-grocery-frontend-standalone
  ```

- Добавляем локальный домен в `/etc/hosts`

  ```bash
  echo '127.0.0.1 lavka.local.yandex.ru' | sudo tee -a /etc/hosts
  echo '127.0.0.1 deli.local.yango.com' | sudo tee -a /etc/hosts
  echo '127.0.0.1 10min.local.market.yandex.ru' | sudo tee -a /etc/hosts
  echo '127.0.0.1 deli.local.yango.yandex.com' | sudo tee -a /etc/hosts
  ```

- Устанавливаем необходимую версию node.js через nvm

  ```bash
  nvm install && nvm use
  ```

- Запускаем `bootstrap` скрипт для настройки проекта

  ```bash
  npm run bootstrap
  ```

- Заходим в свой аккаунт в [тестовом паспорте](https://passport-test.yandex.ru) (если нет аккаунта, то создать и привязать номер телефона).

- Запускаем приложение

  ```bash
  npm run dev
  ```

- Приложение будет доступно на https://lavka.local.yandex.ru

---

## Dev ветка / релизная ветка

Вся разработка идет в dev ветку **lavka-grocery-frontend-standalone/dev**

Ветка **master** резервируется для релизов

Так как по-умолчанию все ПРы создаются на **master**, то добавляется команда создания ПРа: **npm run pr**

```bash
# типовой флоу разработки:
git checkout lavka-grocery-frontend-standalone/dev
git pull origin lavka-grocery-frontend-standalone/dev
git checkout -b lavka-grocery-frontend-standalone/LAVKAWEB-914

# ...пишем код...

git add -A

# в комит копируем название тикета из Стартрека
git commit

git push origin lavka-grocery-frontend-standalone/LAVKAWEB-914

# создаем ПР
npm run pr
```

---

### Для дежурного

1. подготовка релизной ветки

```bash
git checkout lavka-grocery-frontend-standalone/dev
git pull lavka-grocery-frontend-standalone/dev

# могут быть конфликты
git pull origin master

git push origin lavka-grocery-frontend-standalone/dev
# создаем PR на мастер обычным образом
# мерджим в мастер после апрува
# после мерджа надо нажать `Restore branch` так как github удаляет ветки после слияния
```

2. собираем testing и тестируем

3. фиксы багов катим прямо в **master**, возвращаемся в **п.2**

4. катим релиз

## Локальная сборка

|             |                                      |
| ----------- | ------------------------------------ |
| production  | `npm run build`                      |
| development | `NODE_ENV=development npm run build` |

## Генерация типов по api схемам

- Нужно настроить интеграцию с [arcadia](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
- Запуск генерации `npm run typings`
- Информация по генерации типов taxi-typings [тут](https://github.yandex-team.ru/ktnglazachev/taxi-typings)

## TVM (dev)

> Файл .tvm.json нельзя передавать в чатах, нужно использовать [ссылку](https://yav.yandex-team.ru/secret/sec-01exn34gkpwc7y49dd9pfsa4rj) на секретницу

При запуске `npm run bootstrap` всё связанное с tvm будет настроено автоматически, но можно выполнить все шаги вручную, для этого нужно:

- [установить](https://nda.ya.ru/t/jyj6G0nR43rwP4) утилиту `ya`;

- положить последнюю версию файла .tvm.json в корень проекта из [секретницы](https://yav.yandex-team.ru/secret/sec-01exn34gkpwc7y49dd9pfsa4rj), секрет доступен всем из группы «разработка» в ABC [группе разработки фронтенда Яндекс.Лавки](https://abc.yandex-team.ru/services/groceryfrontenddevelopers/).

## Метрика

- Для разработки метрики принято подключать один единственный хук, который пробрасывает все хендлеры метрики
  для страницы и реализует внутри себя необходимые эффекты, выполняемые на странице

События метрики разграничиваются переменной env для разных окружений (stable, testing, unstable, development)

- Для отладки метрики добавляем в url параметр: \_ym_debug=1
  [Дока метрики](https://yandex.ru/support/metrica/code/counter-initialize.html)
