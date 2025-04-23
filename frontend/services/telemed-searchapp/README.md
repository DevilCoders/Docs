# Фронтенд сервиса Телемед Яндекс.Здоровье

Приложение работает в ПП, в браузерах показывается заглушка
с предложением установить или обновить ПП (звонки в ПП доступны с определенной версии)

## Окружение

- node = 8.6.0
- npm = 6.2.0

## Установка

Общий регламент работы с монорепозиторием https://github.yandex-team.ru/serp/frontend-fork

- `cd services/telemed-searchapp/`
- `npm ci`

## Сборка

- `npm run build`

## Запуск

- `npm run dev` - локальный

либо

- `npm run dev:public` - публичный

Куда смотрит фронт?

https://github.yandex-team.ru/search-interfaces/frontend/blob/master/services/telemed-searchapp/src/config/index.ts#L4

## Тесты

### hermione

- `npm run hermione` - в консоли

либо

- `npm run hermione:gui` - в браузере

Куда смотрит фронт при сохранении дампов?

https://github.yandex-team.ru/search-interfaces/frontend/blob/master/services/telemed-searchapp/.config/clement/config.js#L7


## Релиз

- `npm run deploy:qloud` - создает и пушит докер контейнер в registry
- применить загруженный контейнер в проекте Qloud 
выбрав нужное окружение и компонент 
https://qloud-ext.yandex-team.ru/projects/med/  

## Архитектура

Приложение имеет flux архитектуру 
с использованием стейт менеджера redux и мидлвары redux-sagа

Основные требования:

- компоненты должны быть максимально простыми FC
- к стору компоненты коннектятся внутри компонента в папке connected
- преобразования данных из стора производятся в connect
- в селекторах данные берутся из стора, опционально фильтруются, но не преобразовываются
- вся логика должна быть в сагах
- один экран = одна сага
- тайпинги хранятся по месту использования

## API

### Backend

https://dev.med.yandex.ru/telemed/api/v20/

### ПП

- android https://wiki.yandex-team.ru/mobilesearch/app/android/design/jsapi/


## Интрументы

### линтер

Используется общий линтер монорепы, из корня репозитория: 

- `npm run lint`

### размер бандла

- `npm run build:analyze`

### redux-devtools

Для использования необходимо установить [расширение для браузера](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=ru).
Активен в development и testing сборках
