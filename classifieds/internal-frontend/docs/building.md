# Сборка

Проекты собираются в [teamcity](https://t.vertis.yandex-team.ru/project.html?projectId=internal), после чего собранный там docker-образ пушится в registry, откуда скачивается и используется [Шивой](https://docs.yandex-team.ru/classifieds-infra/deploy/quick-start) для последующего деплоя.
