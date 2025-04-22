# Nest template

Генератор проекта под yeoman

## Перед генерацией проекта

1. [Создать сервис на ABC (если нет)](//TODO)
1. [Создать ssl сертификат для локальной разработки](https://wiki.yandex-team.ru/bliss/next-template/docs/#zapuskservisanahttps)
1. [Завести tvm приложения и запросить доступ к blackbox](//TODO)
1. Найти или [завести бакет в s3](//TODO)

## После генерации

1. Закинуть сертификаты private.pem и public.pem в папку ssl
2. Закинуть .tvm.json в корень проекта

## Как использовать
Заводим файл ~/.npmrc с
```
registry=http://npm.yandex-team.ru
```
Далее
```
// Создаем папку с будущим проектом и переходим в нее
mkdir my-project
cd my-project
// Генерируем проект
npm init yo @yandex-int/nest-template
```

Далее ответить на вопросы. Инструкции по запуску будут в README.md сгенерированного проекта

## Примеры использования

- [Контест участника](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/services/contest-participant)
- [Sigma](https://github.yandex-team.ru/skills/sigma)
