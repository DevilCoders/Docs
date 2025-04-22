# Шаблон Open API спецификации для микросервиса

## Описание

- протокол микросервиса описывается в соответствии со спецификацией [OpenAPI 3.0 Specification](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md)
- файл спецификации имеет константное название `openapi.yaml` и находится в директории `proto/spec` в корне проекта
- интерактивная документация протокола реализуется при помощи библиотеки [ReDoc](https://github.com/Redocly/redoc), а также онлайн-редактора `Swagger UI`
- в Аркадии в `billing/coredocs/protodocs/proto/_template` лежит шаблон спецификации и инструментов, шаблон можно скопировать себе в директорию сервиса
- в `billing/coredocs/protodocs/proto/_template/spec/openapi.yaml` лежит пример невалидной с точки зрения линтера опенапи спецификации
- в `billing/coredocs/protodocs/proto/_template/web/index.html` лежит шаблон ReDoc
- TODO: написать make-файл для билда клиентов

## Предварительная установка

- удостоверяемся что в системе установлен `node`
- в директории шаблона `billing/coredocs/protodocs/proto/_template`:
- устанавливаем `ReDoc CLI` глобально
```bash
npm install -g @redocly/openapi-cli@latest
```
- устанавливаем зависимости
```bash
npm -i
```
- TODO: CI в Аркадии и деплой в облако

## Инструменты

- запускаем веб-сервисы онлайн-редактора и доки
```bash
npm start
```
- после запуска будут доступты `swagger-editor` по адресу [http://localhost:8080/swagger-editor/](http://localhost:8080/swagger-editor/) и онлайн-документация [http://localhost:8080](http://localhost:8080)
- все изменения в `swagger-editor` сохраняются в локальный файл `spec/openapi.yaml`

## Команды

- валидация спеки и запуск линтера
```bash
npm run test
```
- деплой документации в `web_deploy`
```
npm run build
```

## Структура каталогов

- пример структуры каталогов

```
.
├── README.md
├── _template
│   ├── package.json #зависимости ноды
│   ├── spec
│   │   └── openapi.yaml #Open API спека сервиса
│   ├── web
│   │   └── index.html #Шаблон ReDoc
│   └── web_deploy #директория для билдов документации и деплоя
```
