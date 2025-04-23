# promo-webvisor-2015

Благодаря платформе [magicdev](https://github.yandex-team.ru/toolbox/magicdev#Что-это-зачем-и-как-этим-пользоваться), проект разрабатывается локально.

Для работы потребуется _Node.js 8_ – устанавливаем его по необходимости:

```bash
brew install nvm
nvm install 8
```

Для старта разработки необходимо cкопировать файл `.tvm-example.json` под именем `.tvm.json`. Вставить в поле секрет tvmSecret из [секретницы](https://yav.yandex-team.ru/secret/sec-01dc2dvq8yndznpdschgx7zks9/explore/versions).

Далее устанавливаем зависимости и запускаем проект:

```bash
npm run deps

# Magicdev запросит ваш пароль, чтобы запустить на 443 порту
npm run dev
```

Проект становится доступен по адресу:
https://localhost.msup.yandex.ru

### Автоматическая перезагрузка страниц в браузере по изменению файлов

Для того, чтобы включить такое поведение,  
необходимо в файле .magicdev.json включить опцию __reload__.

Под капотом используется [Browser Sync](https://browsersync.io/).

## Выкладка в прод
- Пушим в мастер актуальную версию
- Идём в [deploy](https://deploy.yandex-team.ru/stages/metrika-frontend-promos/config/du-welcome/box-welcome) и смотрим текущую версию, используемого докер образа.
- Клонируем и запускаем [таску сборки образа](https://sandbox.yandex-team.ru/task/1285763658/view), в двух местах подставляя версию, инкрементную проду.
- Клонируем и запускаем [таску загрузки статики](https://sandbox.yandex-team.ru/task/1285781120/view), указав ту же самую версию что и в прошлой таске.
- Идём в [deploy](https://deploy.yandex-team.ru/stages/metrika-frontend-promos/config/du-welcome/box-welcome), редактируем конфиг указав новую версию.
