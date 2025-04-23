# expert-front [![Build Status](https://drone.yandex-team.ru/api/badges/expert/expert-front/status.svg)](https://drone.yandex-team.ru/expert/expert-front)

## Запуск

1. Благодаря платформе [magicdev](https://github.yandex-team.ru/project-stub/magicdev#Что-это-зачем-и-как-этим-пользоваться), проект разрабатывается локально.  

2. Создать в корне файл `.env` со следующим содержимым:
    ```
    JWT_PROCTORING_SECRET=${jwt_key}
    ```
    где `jwt_key` можно взять из последней версии [секрета](https://yav.yandex-team.ru/secret/sec-01d7hgy3yc0k0en97zwpe1n9jq/explore/versions) в секретнице.

3. В корне проекта выполнить:

	```bash
	npm run deps
	npm run dev
	```

4. Проект становится доступен по адресу: https://localhost.msup.yandex.ru/adv/expert

5. Для того, чтобы работала авторизация, необходимо залогиниться в тестовом паспорте (https://passport-test.yandex.ru/). Советую разрабатываться в отдельном браузере, так как продовые и тестовые куки сильно несовместимы.

Локальный запуск тестов: 
```bash
cd server
npm run test
```

## Ссылки

Ya.Deploy: https://deploy.yandex-team.ru/projects/expert-front

Tanker: https://tanker.yandex-team.ru/?project=expert-v2

Бункер: https://bunker.yandex-team.ru/expert/

##Gemini

Для того что бы запустить gemini-тесты **локально** нужно выполнить команды: 
```bash
cd static
npm run gemini-gui-desktop
```
Если тесты не прошли по причине новых изменения в верстке(плановые изменения) - нужно сделать скриншоты **эталонными**, нажав на кнопку "accept" 
и закоммитить эти изображения.

Для более быстрой отладки локально можно собирать файлы командой `cd static && npm run gemini-build` и открывать html(`/static/gemini/desktop.gemini/html`) в браузере.

Расположение файлов:
* Все файлы(js, css, html) собираются в папку `static/gemini/{platform}.gemini`
* Эталонные скриншоты находятся в папке `static/gemini/{platform}.screens`
* Конфиг для gemini-тестов находится в файле `/static/{platform}.gemini/common/.gemini.json`

###Объявление переменных

Если переменная является константой - используем `const`, и пишем в uppercase. Так же `const` используется для объявления модулей.
Для всех остальных переменных используем старый добрый `var`.
```javascript
const _ = require('lodash');
const TIME_LIMIT = 200;
```

###Стрелочные функции

Стрелочные функции используем только в колбэках, чтобы код выглядел чище.
```javascript
Object
    .keys(data)
    .forEach(key => {
        data[key] = data[key].toJSON();
    });
```
или
```javascript
Object
    .keys(data)
    .forEach((key, index) => {
        data[key + index] = data[key];
    });
```

## Настройка мониторингов qloud и mdb

1. [Получаем токены](https://github.yandex-team.ru/toolbox/monitorado#%D0%A2%D0%BE%D0%BA%D0%B5%D0%BD%D1%8B) и кладем в `.env`

1. Меняем по необходимости `.monitorado.yml`

1. Смотрим, что изменилось:

        npx monitorado diff -v

1. Проливаем:

        npx monitorado exec -v
