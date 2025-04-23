# Секреты

Секреты храним в секретнице. Как добавлять, описано [этой доке](https://docs.yandex-team.ru/classifieds-infra/deploy/secret ).

Для доставки секретов для локальной разработки и при сборке используем пакет https://github.com/YandexClassifieds/secrets-to-dotenv.

Использование:
1) Добавляем секреты добавляем в `secrets.config.json` (в корне монорепы)
2) Вызываем `npx secrets-to-dotenv`
