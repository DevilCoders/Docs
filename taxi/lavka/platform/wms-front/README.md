## Фронтенд лавки WMS UI

На машине должен быть установлен Yarn https://yarnpkg.com/en/docs/install

### Запуск проекта

#### yarn

`yarn install` - установка зависимостей (делаем единожды или при добавлении нового пакета)

`yarn start` - запуск development версии

`yarn build` - сборка production версии

#### direnv

Настроить direnv (не обязательно). При cd в папку проекта direnv будет сам подгружать env vars, указанные в .envrc

```
cp .envrc.dist .envrc
# edit env vars on your taste
nano .envrc

# install direnv. ubuntu way
sudo apt install direnv

# allows direnv to load env vars automatically
direnv allow
```

### Работа с переводами GetText

Для работы с переводами должен быть установлен GetText https://www.gnu.org/software/gettext/

Тестовая страница с переводом: `/translations-example`

Для скриптов, работающих с переводами, необходимо установить `python3` и установить библиотеку `aiohttp`
`python3 -m pip install aiohttp`

Для обновления переводов: `make generate-translations`\
Предварительно нужно в переменную окружения `TANKER_TOKEN` положить OAuth токен для работы с танкером.\
Токен получить можно тут https://doc.yandex-team.ru/Tanker/api-reference/concepts/request.html \
Будет автоматически создан файл для Танкера, загружен в Танкер и выгружены готовые файлы с переводами в папку проекта.

Для проверки переводов в Танкере: `make check-translations`\
Также можно исключить какой-либо язык из проверки, сделав экспорт переменной `export EXCLUDE_LANGUAGES=`

Процесс переезда ключей с русского языка на английский:\
В ходе работы `make generate-translations` анализируется возможность перехода на новые ключи.\
Сообщения в стандартном выводе скрипта, начинающиеся с `!!!`, описывают детали перехода.\
Если найдены ключи, которые можно перевести на английский язык прямо сейчас, то нужно выполнить
`make update-keys-and-generate-translations`, который

- найдет такие ключи в танкере
- заменит их в исходных файлах фронта на английские
- загрузит новые ключи в танкер
- обновит переводы локально

Корректность замены ключей в исходных файлах нужно проверить перед коммитом.

Конфиг парсера переводов: `./i18next-scanner.config.js`

Конфиг i18n в проекте: `./src/i18n.js`

### Тесты Selenium

#### Запуск тестов

```
# -- из корня проекта. Запускает фронт с моком для тестов.
# Как запустить фронт с полным функционалом, см ниже
make stop_selenium start_selenium

# через docker ps смотрим и ждём пока все сервисы взлетят.
# Бэкэнд стартует особенно долго: 3-5 мин
docker ps

# -- из папки `modules/lavka-fe/`

# нужно один раз при первом запуске
yarn install

# переменные для Пахтеста
export URL=http://frontend-dev:3000 BACKEND_URL=http://localhost:8000 TIMEOUT=5.0

# запускаем один файл
pahtest tests/020-storesPage/040-storesPageEditStore.yml

# запускаем папку
pahtest tests/020-storesPage/

# запускаем в четыре потока
pahtest -j 4 tests/

# запускаем в headless-режиме.
# Работает быстрее и стабильнее, но без vnc
pahtest --headless tests/
```

#### Запуск фронта с полным функционалом

```
# -- из корня проекта
make stop_selenium start_selenium_standalone
```

#### VNC-клиент

**Доступы**

- localhost:5910 - адрес для selenium chrome
- localhost:5911 - адрес для selenium firefox
- пароль: `secret`

Селениум-сервисам на локали можно подключиться через vnc-клиент.
Через клиент в реальном времени можно увидеть поведение браузеров, и даже поучавствовать в нём.

Клиент не работает при запуске Пахтеста в headless-режиме.

**VNC-клиенты**

- На Линуксе хорош tigervnc. Есть в пакетах для Убунту и Арча
  - На Убунту стандартное приложение "Remote Desktop" тоже умеет vnc
- На Винде, Маке - [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/)
  - Он же есть плагином к Хрому

### Деплой

Здесь рассмотрим только специфичные для фронта этапы деплоя. Сам деплой происходит через релизные тикеты, про него в целом сказано [здесь](https://a.yandex-team.ru/projects/lavkawms/code/taxi/lavka/platform/wms-backend?dir=taxi%2Flavka%2Fplatform%2Fwms-backend#deploj).

- На этапе Docker build
  - yarn install
  - Генерятся переводы
    - Подробнее о переводах [здесь](#работа-с-переводами-GetText)
  - yarn build
- После Docker build
  - Собранная через yarn build статика выгружается на S3
- Как работает собранная статика
  - В контейнере с фронтом установлен nginx
    - Фронт запрашивает статику, nginx берёт её из S3 и отдаёт фронту

### Versions
Работа с Версиями
* Используются для статики
* Разные для Тестинга, Прода и Локала
  * Тестинг
    * Формат `1.2.75testing366`
    * Версию проставляет ТимСити при деплое
  * Прод (и Пре тоже)
    * Формат `1.2.75`
    * Версию проставляет ТимСити при деплое
  * CI
    * Формат `5965337a-andrew-zak`
    * Версию проставляет ТимСити при катке CI
  * Локал (dev-машина)
    * Формат `5965337a-andrew-zak`
    * Версию можно получить командой `make version`

### Env types
Типы окружений

#### Env vars list
* APP_ENV
  * Устанавливается
    * хардкодом в makefile, dockerfile
    * в переменных окружения на локальной тачке
  * Значения - `production, testing, ci, local`
*
* REACT_APP_MODE
  * Значения - `production, testing`
  * При сборке забирается из APP_ENV по таким правилам
    * `production -> production`
    * `testing, ci, local -> testing`
  *
* REACT_APP_MODE_REAL
  * Значения - `production, testing, ci, local`
  * При сборке забирается из APP_ENV
  * Несколько Дублирует REACT_APP_MODE
    * Но убирать REACT_APP_MODE пока не стали
    * Будем использовать REACT_APP_MODE_REAL
      когда надо различать окружения testing, ci, local
  *
*
* ENVIRONMENT_TYPE
  * Стандартная переменная у в ТимСити нашем
  * Значения
    * `production` для pre & stable pipelines
    * `testing` для testing pipeline
    * Для PR pipelines - пустая
  *
