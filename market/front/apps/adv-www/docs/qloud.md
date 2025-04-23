## Автоматическая сборка docker-образа и выкладка в Qloud

Проект подготовлен для автоматической сборки docker-образов и выкладки в Qloud.  
Для этого необходимо настроить окружения и выдать права роботам.

#### 1. Сборка docker-образа вручную

1. [Интегрируйте проект с Drone CI](drone.md)

1. Установите и запустите [Docker for Mac](https://download.docker.com/mac/beta/Docker.dmg)

1. Авторизуйтесь в Docker Registry:

  ```bash
docker login -u $USER -p "<ваш OAuth-токен>" registry.yandex.net
  ```

1. Соберите docker-образ и загрузите его в Docker Registry командой `npm run deploy`
 
#### 2. Раздача прав

1. [Запросите права](https://idm.yandex-team.ru/#rf-role=y9mMTEcT#docker/distribution/advertising%7Cadv-front/contributor;;;,rf-expanded=y9mMTEcT,rf=1) уровня _contributor_ для __вашего робота__ на сборку и загрузку в Registry образа _advertising/adv-front_.

1. [Запросите права](https://idm.yandex-team.ru/#rf-role=y9mMTEcT#docker/distribution/advertising%7Cadv-front/viewer;;;,rf-expanded=y9mMTEcT,rf=1) уровня _viewer_ для __robot-cit__ и __robot-qloud-client__ на выкладку образа _advertising/adv-front_ в Qloud.

#### 3. Настройка тестового окружение в Qloud

1. Создайте в проекте __advertising__ приложение с именем __adv-front__

1. В появившемся по-умолчанию окружение __test__ добавьте домен __adv-front.qloud.yandex.ru__

1. Создайте компоненту с именем __www__ типа docker-image и привяжите к ней адрес образа `registry.yandex.net/advertising/adv-front`

  > Не забудте указать сеть и выбрать количество инстансов.

1. Добавьте роут __/__ и свяжите его с компонентой __www__

1. Добавьте переменную окружения `NODE_ENV=testing`

1. Добавьте __robot-cit__ в группу Admin на вкладке «[Access](https://qloud-ext.yandex-team.ru/projects/advertising/adv-front/test?tab=access)»

#### 4. Включение хука на тег в Drone.CI

1. В [настройках репозитория](https://drone.yandex-team.ru/advertising/adv-front/settings) включите опцию «Tag Hooks»

#### 5. Выпуск релиза

Теперь для того, чтобы выпустить релиз необходимо создать тег c версией и запушить его.

Drone автоматически соберёт docker-образ с этой версией,   
а интегрированный [cit-клиент](https://wiki.yandex-team.ru/q/devops/cit-continuous-integration-tool/) автоматически выкатит его в созданное тестовое окружение.

Настройки cit-клиента можно поменять в файле [.cit.json](./.cit.json).
