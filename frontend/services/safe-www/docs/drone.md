## Интеграция с Drone

Проект подготовлен для работы с [Drone CI](https://drone.yandex-team.ru/), но его необходимо активировать.  
Для этого необходимо настроить окружения и выдать права роботу.

Если у вас нет робота 🤖 , заведите нового [через форму на wiki](https://wiki.yandex-team.ru/diy/zombik/#zavestirobota) (логин и пароль придут вам на почту).

#### 1. Получение OAuth-токенов

Для роботы вам понадобится OAuth-токен вашего аккаунта и аккаунта робота.

1. В браузере откройте [oauth.yandex-team.ru](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1) и получите __ваш OAuth-токен__.

1. В приватном режиме браузера откройте [oauth.yandex-team.ru](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1),  
авторизуйтесь реквизитами робота и получите __OAuth-токен робота__.

#### 2. Подготовка окружения

1. Устанавите Drone-клиент:

  ```bash
brew tap drone/drone
brew install --devel drone
  ```

1. Зайдите на [главную страницу](https://drone.yandex-team.ru/) и авторизуйтесь

1. Откройте [страницу Drone-аккаунта](https://drone.yandex-team.ru/account/), нажмите _SHOW TOKEN_ и скопируйте __drone-токен__

1. Сохраните URL-адрес Drone и полученный __drone-токен__ в переменные окружения:

  ```bash
export DRONE_SERVER="https://drone.yandex-team.ru/"
export DRONE_TOKEN="<drone-токен>"
  ```

1. Поместите реквизиты робота в секреты:

  ```bash
export ROBOT_LOGIN="<логин робота>"
export ROBOT_OAUTH_TOKEN="<OAuth-токен робота>"
export REPO_PATH=$((git remote get-url upstream || git remote get-url origin) | cut -d: -f2 | cut -d. -f1)

noglob drone secret add --skip-verify --image=* --event push --event pull_request $REPO_PATH REGISTRY_USERNAME $ROBOT_LOGIN
noglob drone secret add --skip-verify --image=* --event push --event pull_request $REPO_PATH DOCKER_USERNAME $ROBOT_LOGIN
noglob drone secret add --skip-verify --image=* --event push --event pull_request $REPO_PATH REGISTRY_PASSWORD $ROBOT_OAUTH_TOKEN
noglob drone secret add --skip-verify --image=* --event push --event pull_request $REPO_PATH DOCKER_PASSWORD $ROBOT_OAUTH_TOKEN
```

1. Перейдите на [страницу аккаунта](https://drone.yandex-team.ru/account) и нажмите _SYNC LIST_

1. В списке найдите _stardust/safe-www_ и активируйте

1. [Запросите права](https://idm.yandex-team.ru/#rf-role=2Ju4ASBC#docker/distribution/spec%7Cci-tools/viewer;;;,rf-expanded=2Ju4ASBC,rf=1) для вашего робота на образ _spec/ci-tools_

История сборок будет доступна на [странице проекта](https://drone.yandex-team.ru/stardust/safe-www).

#### 3. Проверка пулл-реквестов

Теперь на каждый пулл в Drone будет автоматически запускаться линтинг кода,  
а так же в описание будут добавлены ссылки на задачи найденные в коммитах.

Вы можете дополнить сборку командами,   
добавив одну из предоставляемых [ci-tools](https://github.yandex-team.ru/spec-tools/ci-tools#Сontinues-integration-tools-) – образ с полезными командами для сборки.

Это можно сделать в подсекции _commands_ первой секции _build_ в файле [.drone.yml](./.drone.yml).
