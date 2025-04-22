# stories-api
API для сервиса сторис Авто.ру

# Содержание
1. [С чего начать разработку](#first-steps)
1. [Взаимимодействие с БД](#db-operations)
    1. [Как завести новую модель и табличку в базе](#db-operations-new-model)
    1. [Как изменить существующую модель и соответствующую табличку в базе](#db-operations-edit-model)
    1. [Возможные проблемы](#db-operations-problems)
    1. [Как накатить миграцию на прод](#db-operations-production)
    1. [Полезные команды](#db-operations-useful-commands)
    1. [Кластеры MySQL для авто](#db-operations-clusters-auto)

## С чего начать разработку? <a name="first-steps"></a>
1. Установи зависимости: `npm ci` в корне
2. Запусти dev-сервер. При запуске нужно указать env-переменную `STORIES_API_DOMAIN` для подключения к БД нужного сервиса.
```
STORIES_API_DOMAIN=autoru npm run dev
```
3. ...
4. PROFIT?

### Команды
* `STORIES_API_DOMAIN=autoru npm run dev` запуск node в режиме дебага
* `STORIES_API_DOMAIN=autoru npm start` запуск node (прод режим)
* `make start-db` запуск docker-образа с локальной базой для тестов
* `make stop-db` остановка docker-образа с локальной базой для тестов
* `STORIES_API_DOMAIN=autoru npm run test:run` запуск юнит тестов
* `npm run test:e2e:run` запуск e2e тестов
* `STORIES_API_DOMAIN=autoru npm run test:watch` запуск тестов в watch-режиме (требует запущенной локально базы)

### Сваггер
* [Сваггер](./docs/swagger.md)

## Взаимимодействие с БД <a name="db-operations"></a>
Используем [typeorm](https://github.com/typeorm/typeorm)
[Официальная документация](https://typeorm.io/)

### Как завести новую модель и табличку в базе <a name="db-operations-new-model"></a>
1. В папке модуля создаем файл с именем `<name-of-model>.model.ts`.
Как-то так: 
```
import { ApiProperty } from '@nestjs/swagger';
import {
    PrimaryGeneratedColumn,
    Column,
    Entity,
} from 'typeorm';

@Entity({ name: 'awesome_things' })
export class AwesomeThingModel {
    @PrimaryGeneratedColumn({ unsigned: true })
    id: number;

    @Column({ name: 'arbitrary_field', type: 'varchar', length: '255', nullable: true })
    arbitraryField: string;
    // ... other columns here
}

```
2. Сгенерировать миграцию
```STORIES_API_DOMAIN=autoru NODE_ENV=local npm run typeorm migration:generate -- -n my-incredible-migration```
3. Заглянуть в файл миграции (он находится в `typeorm/migrations/<timestamp>-my-incredible-migration.ts`) и убедиться, что там нет ничего криминального (`DROP TABLE`, например). Миграция генерируется по всем моделям, не только по той, которую ты создал и содержит `sql` команды, которые приводят таблицы базы данных в состояние, соответствующее описанию моделей. Так что если случайно что-то поменял в других моделях, либо схема в базе почему-то отличается от имеющихся моделей, это все найдет свое отражение в файле миграции. При необходимости, можно руками поправить, убрав лишние строчки.
4. Посмотреть что там с миграциями и нет ли чего лишнего среди непримененных миграций
```STORIES_API_DOMAIN=autoru NODE_ENV=local npm run typeorm migration:show```
Крестиками отмечены те, что применены. Не отмечена крестиком должна быть только та миграция, которую ты только что сгенерил.
4. Применить миграцию (точнее, все миграции, которые еще не применены)
```STORIES_API_DOMAIN=autoru NODE_ENV=local npm run typeorm migration:run```
5. Если что-то пошло не так, миграцию можно откатить
```STORIES_API_DOMAIN=autoru NODE_ENV=local npm run typeorm migration:revert```

### Как изменить существующую модель и соответствующую табличку в базе <a name="db-operations-edit-model"></a>
1. Внести изменения в файл модели
2. Сгенерировать миграцию
```STORIES_API_DOMAIN=autoru NODE_ENV=local npm run typeorm migration:generate -- -n my-incredible-migration```
ИЛИ создать ручную миграцию, если ты точно осознаешь, что делаешь:
```STORIES_API_DOMAIN=autoru NODE_ENV=local npm run typeorm migration:create -- -n my-incredible-migration```
3. Проверить файл миграции на наличие каких-то посторонних включений, не связанных с вашими изменениями, если ты ее сгенерировал, или заполнить, если ты создал шаблон для ручной миграции (файл находится в `typeorm/migrations/<timestamp>-my-incredible-migration.ts`).
4. Посмотреть что там с миграциями и нет ли чего лишнего среди непримененных миграций
```STORIES_API_DOMAIN=autoru NODE_ENV=local npm run typeorm migration:show```
Крестиками отмечены те, что применены. Не отмечена крестиком должна быть только та миграция, которую ты только что сгенерил.
4. Применить миграцию (точнее, все миграции, которые еще не применены)
```STORIES_API_DOMAIN=autoru NODE_ENV=local npm run typeorm migration:run```
5. Если что-то пошло не так, миграцию можно откатить
```STORIES_API_DOMAIN=autoru NODE_ENV=local npm run typeorm migration:revert```

### Возможные проблемы <a name="db-operations-problems"></a>
1. `nullable` поля, которые перестали быть таковыми, потребуют допиливания автомиграции руками - там надо будет проставить какие-нибудь дефолтные значения.

### Как накатить миграцию на прод <a name="db-operations-production"></a>
1. Сходи в [секретницу](https://yav.yandex-team.ru/?tags=vsif,mysql), возьми пароль для прода и замени его в соответствующей переменной в `.env` в корне проекта.
2. Сходи в продовый кластер, возьми оттуда адреса хостов и проставь в конфиге `./configs/domains/autoru/production.js`
3. `STORIES_API_DOMAIN=autoru NODE_ENV=production npm run typeorm migration:run`

### Полезные команды <a name="db-operations-useful-commands"></a>
Внимание! Перед запуском обязательно указать env переменные `STORIES_API_DOMAIN` и `NODE_ENV`.
Пример: `STORIES_API_DOMAIN=autoru NODE_ENV=local npm run typeorm migration:show`
* `npm run typeorm migration:show` - список миграций, крестиком отмечены уже примёненные
* `npm run typeorm migration:create -- -n <migration-name>` - создание шаблона для миграции, запускай, если хочешь писать ее руками
* `npm run typeorm migration:generate -- -n <migration-name>` - автоматическая генерация миграции на основе модели 
* `npm run typeorm migration:run` - запуск всех миграций
* `npm run typeorm migration:revert` - откат последней запущенной миграции

### Кластеры MySQL для авто <a name="db-operations-clusters-auto"></a>
* [dev](https://yc.yandex-team.ru/folders/foo4nrk07dl14udeb4js/managed-mysql/cluster/mdbf6nbtcc7u0bo3k2nf)
* [test](https://yc.yandex-team.ru/folders/foo4nrk07dl14udeb4js/managed-mysql/cluster/mdbq9mb11u9cpe4cfe1j)
* [prod](https://yc.yandex-team.ru/folders/foo4nrk07dl14udeb4js/managed-mysql/cluster/mdbq9mb11u9cpe4cfe1j)
