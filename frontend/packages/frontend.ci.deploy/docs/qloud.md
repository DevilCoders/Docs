# Deploy в Qloud

Деплоит готовый docker-образ в qloud.<br>
Для подготовки окружения и деплоя использует ручку https://platform.yandex-team.ru/api/v1/environment


## Переменные окружения
- `QLOUD_OAUTH_TOKEN` - qloud token
- `DOCKER_OUATH_TOKEN` - docker oauth token для работы с `registry.yandex.net`
- `DEPLOY_VERSION` - docker image version

## Формат конфига
Формат конфигурационного файла описан [здесь](../src/deploy-scripts/qloud/)
```(json)
{
    "type": "qloud",
    "beta": {
        "QLOUD_PRJ_NAME": string, // имя проекта в Qloud
        "QLOUD_APPLICATION_NAME": string, // имя приложения в Qloud
        "QLOUD_ENV_NAME": string, // по умолчанию - "pr-${process.env.TRENDBOX_PULL_REQUEST_NUMBER}"
        "QLOUD_TEMPLATE_ENV_NAME": string, // название шаблона окружения для бет, которое будет форкаться каждый раз при заведении окружения для новой беты
        "QLOUD_COMPONENT_NAME": string, // имя компонента в Qloud, который будет обновлен
        /**
        * Домен, под которым будут расположены беты.
        * Пример BETA_DOMAIN_SUFFIX: safety.pr.yandex.ru
        * Пример полного имени беты:
        *   - `${QLOUD_ENV_NAME}.${BETA_DOMAIN_SUFFIX}` = "pr-8651.safety.pr.yandex.ru"
        */
        "BETA_DOMAIN_SUFFIX": string, // окончание доменного имени после QLOUD_ENV_NAME. Пример: "safety.pr.yandex.ru",
        /**
        * Имя балансера или "L7" или "cdn". Окружение должно иметь право доступа к балансеру.
        * Используется в ручке https://wiki.yandex-team.ru/qloud/doc/api/domains/#create
        * Пример: 'webmaster-testing-balancer'
        */
        "BETA_DOMAIN_TYPE": string;
        /* 
         * Необязательное значение.
         * Ставить, если нужен только деплой qloud environment, без апдейта компонента.
         * Если выставлено в true, переменные DOCKER_IMAGE_REPO_NAME и прочее для update компонента будут проигнорированы
         */
        "QLOUD_PREPARE_ONLY": boolean;

        "DOCKER_IMAGE_REPO_NAME": string, // имя докер-репозитория, где хранятся образы
    },
    "release": {
        "QLOUD_PRJ_NAME": string, // "webmaster",
        "QLOUD_APPLICATION_NAME": string, // "safety-l7-www",
        "QLOUD_ENV_NAME": string, // "test",
        "QLOUD_COMPONENT_NAME": string, // имя компонента в Qloud, который будет обновлен
        "DOCKER_IMAGE_REPO_NAME": string, // имя докер-репозитория, где хранятся образы
    }
}
```

## Как работает скрипт

### Подготовка к деплою пулреквестных бет
Для пулреквестных бет нужно один раз (если еще нет) создать в Qloud приложение и шаблонное окружение с именем из QLOUD_TEMPLATE_ENV_NAME.

Настройки шаблонного окружения обычно соответствуют окружению для тестинга. Настраивать там домен не нужно, а в качестве докер-образа для компонента можно указать что угодно.

Убедиться нужно лишь, что у приложения для бет есть права на использование балансера из BETA_DOMAIN_TYPE.

### Деплой в Qloud выполняется в 2 этапа:
#### Подготовка среды (только при деплое бет):
- проверка наличия окружения;
- создание окружения, если его нет;
- добавления домена в окружения;
- деплой окружения
#### Обновление компонента:
- получает текущее окружение по имени;
- получает хэш докер образа переданной версии (DEPLOY_VERSION);
- обновляет версию компонента в Qloud;
- проверяет то, что версия задеплоилось
