# env-utils

Пакет для получения данных из переменных окружения. Умеет логировать полученные данные в зашифрованном виде. В настоящее время используется в различных CI-инструментах.

Установка:

```
npm install @yandex-int/si.ci.env-utils
```

Пример получения переменной ENV_NAME и логирования её в зашифрованном виде:

```(typescript)
import { getEnvWithSecretOr } from "@yandex-int/si.ci.env-utils";

const someEnv = getEnvWithSecretOr('ENV_NAME', 'default-value')
```

если переменная не определена, по умолчанию будет использовано `default-value`.

При запуске этого кода с env `DEBUG=serp:env-utils` В консоли будет выведено:

```
serp:env-utils "ENV_NAME" environment variable is defined; using "encrypted: pKw...9M="
```

Расшифровать зашифрованное значение можно с помощью [приватного ключа](https://yav.yandex-team.ru/secret/sec-01e8r2c0cdpf5te56gghzg1f93/explore/versions), доступ к которому есть только у команды FEI.
