# Разработка

## Пререквизиты
1. `node >= 12.20.0`
2. `mongodb < 3.6` (не точно, вроде с 4.4.2 сработало)

## Первые шаги
1. Склонировать проект

```bash
 git clone git@github.yandex-team.ru:devexp/devexp.git
```

2. Установить зависимости

```bash
npm ci
```

3. Запустить

```bash
npm start
```

## Тестирование

* юнит тесты `npm test`
* е2е тесты `npm run test:e2e`
* nock тесты `npm run test:nock`

## Необязательный шаг

Если нужно сохранять дампы для nock-тестов и отлаживаться с реальными запросами.

Создать файл `config/secret.json` с токенами для github/staff/startrek.

    {
      "services": {
        "github": {
          "options": {
            "auth": {
              "type":  "token",
              "token": ""
            }
          }
        },

        "yandex-staff": {
          "options": { "token": "" }
        },

        "yandex-startrek": {
          "options": { "token": "" }
        }
      }
    }

Для GitHub токен можно сгенерировать [здесь](https://github.yandex-team.ru/settings/tokens).

Для staff/startrek токен может быть одинаковый, узнать как его получить можно [тут](https://wiki.yandex-team.ru/intranet/dev/oauth/#poluchenietokena). Например, можно получить [так](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ff39dc1f2692463ab9dc806e3d2fec5e)

## Отладка
Ревьюшница работает в основом с веб-хуками, чтобы что-то начало происходить, нужно отправить POST-запрос на поднятый локально http-сервер.
Чтобы проверить, что ваш код работает, скорее всего вам нужно отправить хук.

Есть два пути, как можно это сделать:
1. Использовать [ngrok](https://ngrok.com/), настроить локальный туннель на свою машину, и настроить новый хук в тестовом репозитарии на адрес ngrok'a
2. Сохранить уже отправленный webhook в отдельный файл json и отправлять его на локальный сервер так `./tools/webhook.sh webhook.json`
