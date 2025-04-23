[![N|Solid](https://jing.yandex-team.ru/files/excel/2016-11-28_21.20.17.png)](https://nodesource.com/products/nsolid)

# samadhi-toloka
Данный проект помогает разрабатывать шаблоны **samadhi** для Яндекс.Толока.
Включает в себя два инструмента:

  - Локальный запуск шаблона на задании из выброного проекта -> пула
  - Деплой шаблона на указаный проект

# Инициализация и запуск

#### Получение токена
Окружения Толоки:
  - **sandbox** - [sandbox.toloka.yandex.ru](https://sandbox.toloka.yandex.ru/)
  - **prod** - [toloka.yandex.ru](https://toloka.yandex.ru/)

Окружения Янга:
  - **sandbox** - [sandbox.yang.yandex-team.ru](https://sandbox.yang.yandex-team.ru/)
  - **prod** - [yang.yandex-team.ru](https://yang.yandex-team.ru/)
  
[Токены лежат здесь](https://yav.yandex-team.ru/secret/sec-01cn53b0mcf16njk1haxjrzp3n/explore/versions)

Также получить токены можно в личном кабинете, как это сделано описано [на странице документации Яндекс.Толока](https://tech.yandex.ru/toloka/doc/concepts/access-docpage/).

#### Инициализация токенов
В корне (на уровне package.json) необходимо создать файл **samadhi.secret.json** со следующим содержимым:
```json
{
  "sandbox": "Ваш токен для sandbox Толоки",
  "production": "Ваш токен для production Толоки",
  "yang-sbox": "Ваш токен для sandbox Янга",
  "yang-prod": "Ваш токен для production Янга"
}
```

#### Инициализация заданий
Задания можно скачать из существующего пула. Для этого необходимо использовать следующую команду:
```sh
npm run scenario:clone-pool -- --mode <TOLOKA_ENV: sandbox | production> --pool <POOL_ID>
```
  
#### Запуск проекта
Для запуска необходимо выолнить следующие команды
```sh
npm run scenario:build
npm run scenario:ttk:server
npm i
open https://localhost:9001
open https://localhost:8083/assets/script.js
```
В открывшихся вкладках может потребоаться сделать исключение по безопасности. Сделать это нужно как для дев сервера вебпака так и для сервера толоки. основное приложение будет открыто по первой ссылке.

# Деплой шаблона
##### Деплой на конкретный проект:
```sh
npm run scenario:build-release
npm run scenario:deploy -- --mode <TOLOKA_ENV: sandbox | production | yang-sbox> --project <PROJECT_ID>
```

##### Деплой на список проектов:
Деплой на список проектов используется с помощью файла **samadhi.deploy.batch.json**. Там описаны гурппы проектов, которые можно раздеплоить.
```sh
npm run scenario:build-release
npm run scenario:deploy-batch -- --key <BATCH_KEY>
```

##### Обновление спецификации шаблона:
Для обновления спецификации input и output данных шаблона нужно описать новую структуру данных в файле [io-specs.js](/io-specs.js) и вызвать команду:
```sh
npm run scenario:update-specs -- --mode <TOLOKA_ENV: sandbox | production | yang-sbox> --pool <POOL_ID>
```

#### Комменты по поводу улучшения
- почему ты не используешь? https://github.com/bem/bem-react/tree/master/packages/classname
- почему ты не используешь на fs нейминг по БЭМ? Тебе удобно открывать 10 index.ts?
- если у тебя кроме render ничего нет, то это может быть простой Stateless Component. В большинстве случаев может. Напимер тут https://github.yandex-team.ru/mm-interfaces/samadhi-toloka-scenario/blob/master/src/components/button/index.tsx Но у тебя вообще везде можно 😉
- не используй export default. Это приводит к неконтролируемому переименованию классов по проекту.
- 'typings/radio-group-item' типы компонентов надо держать рядом с компонентами
- почему у тебя где-то CSS селекторы, а где-то CSS модули?
- не используй arrow-ф-ции в обработчиках (value: string) => onChange && onChange(value), это приводит к созданию новой ф-ции на каждый render
- для того чтобы этого https://github.yandex-team.ru/mm-interfaces/samadhi-toloka-scenario/blob/master/src/components/task/index.tsx#L21 не существовало более, мы сделали https://github.com/bem/bem-react/tree/master/packages/core
- с контейнерами всё +- чотко 😉
