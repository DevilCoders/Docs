###### Сборка проекта:

- Обновить версию `debian/changelog`
- Выполнить `npm run release`

###### Деплой пакета:

- Состоит из двух частей: статика (стили, картинки) и подключаемые файлы (переводы, конфиг)
- Статика катится автоматически после вливания ПР в master. Для этого используется trendbox + s3
- Подключаемые файлы собираются в TeamCity (https://teamcity.yandex-team.ru/viewType.html?buildTypeId=PassportFrontend_Passport_AuthCustoms) и далее выкатываются через Кондуктор (https://c.yandex-team.ru/packages/yandex-passport-auth-customs) по аналогии с Паспортным пакетом

###### Создание контейнер-ресурса в Sandbox:

_всё это нужно на случай если случились проблемы с текущим ресурсом_

- Заходим в Sandbox.yandex-team.ru
- Жмем "Create a new task"
- Выбираем TRENDBOX_CI_LXC_BETA и жмем "Create"
- В "Description" пишем любое человеко-понятное описание пакета, например: "PASSPORT AUTH CUSTOMS"
- В "Shell script to execute during final stage" пишем: 
```
curl -O https://bootstrap.pypa.io/get-pip.py
python get-pip.py --user
export PATH=~/.local/bin:$PATH

pip install --upgrade -i https://pypi.yandex-team.ru/simple/ pip
pip install -i https://pypi.yandex-team.ru/simple/ awscli==1.16.14
```
- В "Components" выбираем "node_js"
- В "Ubuntu release" выбираем 'trusty'
- Жмем "Run"
- По окончанию сборки контейнера заходим в раздел "CHILD TASKS"
- Находим подзадачу SANDBOX_LXC_IMAGE и переходим в нее
- Заходим в раздел "RESOURCES"
- Находим там наш ресурс под названием TRENDBOX_CI_LXC_IMAGE_BETA
- Копируем номер ресура в файл проекта `.trendbox.yml` в значение свойства `container_resource`

###### Автоматический ресайз изображения:

Пример вызова:

```
npm run resize -- ./tools/resize.jpg 0 jpg
```

После исполнения скрипта в консольке будет следующее:

```
Image ./tools/resize.jpg resized to 1024px width and saved in ./i/0/bg_1024w.jpg
Image ./tools/resize.jpg resized to 1280px width and saved in ./i/0/bg_1280w.jpg
Image ./tools/resize.jpg resized to 1440px width and saved in ./i/0/bg_1440w.jpg
Image ./tools/resize.jpg resized to 1680px width and saved in ./i/0/bg_1680w.jpg
Image ./tools/resize.jpg resized to 1920px width and saved in ./i/0/bg_1920w.jpg
```

Значения filename, number и ext, указанные в примере вызова, являются значениями по умолчанию.