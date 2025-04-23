# Система конфигурации

## Использование

Описываем структуру конфига для сервиса:

```typescript
import { ConfigField, ValidatorKind } from '@server-libs/configurator/metadata';

class DBConfig {
    // обычное скалярное поле
    @ConfigField()
    user!: string;

    // опциональное поле
    @ConfigField({ isOptional: true })
    password?: string;

    isAwesome(): boolean {
        return true;
    }
}

class ApiConfig {
    // скалярное поле number который можно использовать как TCP порт
    @ConfigField({ validator: ValidatorKind.Port })
    port!: number;
}

export class MetrikaAppConfig {
    // вложенное поле
    @ConfigField()
    apiConfig!: ApiConfig;

    // в валидатор для поля можно передавать функцию
    @ConfigField({
        validator: (dbc: DBConfig) => dbc.isAwesome(),
    })
    dbConfig!: DBConfig;
}
```

Получаем инстанс конфига:

```typescript
import { getConfig } from '@server-libs/configurator/configurator';

const config = await getConfig(MetrikaAppConfig);
config.dbConfig.user; // string
```

## Валидаторы

Есть встроенные валидаторы `ValidatorKind` для типов данных, которые часто можно встретить в конфиге приложения:

-   `ValidatorKind.Url` - поле должно быть валидным URL
-   `ValidatorKind.Port` - поле должно быть валидным TCP портом
-   `ValidatorKind.IpAddress` - поле должно быть валидным IP адресом

Использование:

```typescript
export class MetrikaAppConfig {
    @ConfigField({ validator: ValidatorKind.Port })
    port!: number;
}
```

Важно: валидаторы не проверяют, что поле в конфиге имеет правильный тип данных (например string или number), а
вызываются после проверки на правильность типов с целью убедится что поле записанно в правильном формате (например в
примере выше сначала пройдёт проверка что `port` - это валидный number, а затем - что значение поля `port` располагается
в правильном числовом интервале, чтобы его можно было использовать как TCP порт).

Как валидатор можно также использовать функцию для более тонкого контроля:

```typescript
class DBConfig {
    @ConfigField()
    user!: string;

    @ConfigField()
    password!: string;

    isValid(): boolean {
        return this.password.length > 3;
    }
}

export class MetrikaAppConfig {
    @ConfigField({
        validator: (dbc: DBConfig) => dbc.isValid(),
    })
    dbConfig!: DBConfig;

    @ConfigField({
        validator: password => password.length > 3,
    })
    password!: string;
}
```

В функцию в качестве 1го аргумента передаётся инстанс класса конкретного поля (либо значение этого поля для скалярных
типов), если функция вернет `true` значит поле валидно, если `false` - невалидно.

## Способы конфигурации

Можно использвать следующие YAML файлы, которые будут смержены с `env.base.yml` в зависимости от окружения:

-   `env.production.yml` (для `production` окружения)
-   `env.development.yml` (для локальной разработки, не под контролем версий)

Сначала беруться настройки из `env.base.yml` и переопределяются настройками из конфигов для окружения
(`env.production.yml`, `env.development.yml`). Также можно перезаписывать вложенные поля, например:

📂 `env.base.yml`

```yaml
dbConfig:
    user: login
    password: pwd
```

📂 `env.production.yml`

```yaml
dbConfig:
    password: killerisjim
```

На выходе получаем:

```yaml
dbConfig:
    user: login
    password: killerisjim
```

Структура YML файла должна повторять структуру описанную ранее в классе конфига (e.g. в классе `MetrikaAppConfig`).

## Переменные окружения

Значения в конфиге могут включать в себя значения переменных окружения:

```yaml
source:
    url: https://my.url.com/{{SERVICE}}/foo
```

Чтобы такая конструкция, заключённая в `{{}}`, была заменена переменной окружения, необходимо описать её в классе
конфига:

```typescript
@ConfigField({ envSubstitutionParams: {
    name: 'SERVICE',
    options: ['appmetrica', 'shopper'],
}})
url!: string;
```

Ещё через переменные окружения можно задать значения при помощи специального синтаксиса, повторяющего схему yaml файла,
например:

```bash
env apiConfig.port=90 npm run start # ...service name
```

Важно: значения переданные через переменные окружения будут иметь самый высокий приоритет и будут перетирать поля в
конфигах для окружения (`env.production.yml`, `env.development.yml`), например:

📂 `env.base.yml`

```yaml
dbConfig:
    user: login
    password: pwd
    replicaSet: secondary
```

📂 `env.production.yml`

```yaml
dbConfig:
    password: killerisjim
    replicaSet: primary
```

```
env dbConfig.password=secret npm run start
```

На выходе получаем:

```yaml
dbConfig:
    user: login
    password: secret
    replicaSet: primary
```
