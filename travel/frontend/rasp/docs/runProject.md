# Запуск проекта

Разработка проекта ведется локально. Так же можно запустить локально docker-контейнер со всем приложением.

На данный момент проект работает на nodejs@8.14.1.

## Перед запуском

Смонтировать [Аркадию](https://docs.yandex-team.ru/devtools/) и открыть проект в папке `travel/frontend/rasp`

Добавить в `/etc/hosts` хосты для локальной разработки:

```bash
#local-rasp-development
127.0.0.1 l.rasp.yandex.ru
127.0.0.1 l.t.rasp.yandex.ru
127.0.0.1 l.rasp.yandex.ua
127.0.0.1 l.t.rasp.yandex.ua
127.0.0.1 l.rasp.yandex.by
127.0.0.1 l.t.rasp.yandex.by
127.0.0.1 l.rasp.yandex.kz
127.0.0.1 l.t.rasp.yandex.kz
127.0.0.1 l.rasp.yandex.uz
127.0.0.1 l.t.rasp.yandex.uz
```

Ставим зависимости проекта (ставим именно такой командой, потому что помимо установки зависимостей в ней могут выполняться и другие задачи):

```bash
npm run deps
```

В WebStorm следующие папки метим, как **excluded** для ускорения индексирования:

-   log

## Запуск локально

```bash
# запуск мобильной и десктопной версии
npm run local
# запуск только десктопной версии
npm run local-desktop
# запуск только мобильной версии
npm run local-mobile
```

После этого переходим по адресу [https://l.rasp.yandex.ru:3000](https://l.rasp.yandex.ru:3000)

### Если при запуске появляется ошибка сертификата

Нужно перевыпустить сертификат и положить его в проект:

1. Идем в https://crt.yandex-team.ru/certificates
2. Жмакаем "Заказать сертификат"
3. Заполняем форму:
    1. CA name -> InternalCA
    2. Extended Validation -> no
    3. Желаемый TTL (в днях) -> 10000
    4. Common name -> l.rasp.yandex.ru
    5. Хосты -> l.rasp.yandex.ru,l.t.rasp.yandex.ru,l.rasp.yandex.ua,l.t.rasp.yandex.ua ,l.rasp.yandex.by,l.t.rasp.yandex.by,l.rasp.yandex.kz,l.t.rasp.yandex.kz,l.rasp.yandex.uz,l.t.rasp.yandex.uz
    6. ABC-сервис -> Фронтенд Яндекс.Путешествий
    7. ECC сертификат -> no
4. Далее в поле фильтра "Владелец" вбиваем свой логин и ищем сертификат с Common name "l.rasp.yandex.ru" (скорее всего он будет первым в списке)
5. Жмакаем на него и скачиваем (появится иконка загрузки в правом верхнем углу)
6. Кладем этот файлик в проект, чтобы он был доступен по пути "certs/l.rasp.yandex.ru.pem"
7. Коммити, создаем ПР и мерджим в trunk

## Фиксация версии nodejs при разработке

Чтобы в дальнейшем не было проблем из-за разности в версии nodejs, которая используется при разработке и той, что будет работать в фоне, лучше поставить [nvm](https://github.com/nvm-sh/nvm). А затем добавить скрипт для автоматического переключения версии nodejs для конкретной папки с проекта в `~/.bash_profile`:

```
# nvm common settings
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

# nvm settings for projects
if [ "$PWD" == "/projects/morda_front" ]
  then nvm use 8.14.1
fi
```

Не забудьте поменять путь к директории, в которой у вас лежит проект.

## Настройки

Можно указать свой бэкенд, указав переменную окружения BACKEND_HOST при запуске:

```bash
BACKEND_HOST={your-backend-url} npm run local
```

Таким же образом можно переопределить и другие переменные.

## Установка плагина DevTools

https://github.com/zalmoxisus/redux-devtools-extension - для того чтобы иметь возможность просматривать текущий Store
и события диспатчера, нужно установить этот Chrome Extension ( норм работает в Yandex Browser )

## Настройка доступа из parallels

Иногда возникает необходимость посмотреть сайт, используя windows-среду или какой-то
специфичный для нее браузер (привет IE).

Для этого нужно в настройках сети parallels выбрать "Общая сеть" в "Источник", затем зайти в
дополнительные настройки сети и открыть сетевый настройки. Адрес хостовой машины как правило
имеет значение, которое можно вычислить как значение поля "Начальный адрес" + 1. Обычно это
`10.211.55.2`. Нужно вписать этот адрес в hosts.txt файл в parallels. Для этого идем по адресу
`C:\Windows\System32\drivers\etc` и добавляем в hosts:

```text
10.211.55.2     l.rasp.yandex.ru
10.211.55.2     l.t.rasp.yandex.ru
```

Так же можно добавить и другие домены, что записаны в hosts на хостовой машине.

## Сборка и запуск Docker-контейнера

Не забудьте заменить путь с учетом расположения проекта на вашем компьютере.

```bash
docker build -t=morda_front --build-arg RASP_CONTAINER_RUN_LOCALLY=1  ./
docker run -p=443:443 --env-file=/Users/makc-brain/Projects/morda_front/docker/env/testing.txt morda_front
```

Так же можно иметь локальный файл с дополнительными перемеными окружения: `morda_front/docker/env/local.txt` (файл добавлен в `.gitignore`)
Команда для запуска с дополнительным файлом:

```bash
docker run -p=443:443 --env-file=/Users/makc-brain/Projects/morda_front/docker/env/testing.txt --env-file=/Users/makc-brain/Projects/morda_front/docker/env/local.txt morda_front
```

Если вы хотите собрать контейнер не для локального запуска, а для каких-то
других целей, то используйте команду без дополнительных переменных:

```bash
docker build -t=morda_front ./
```

Зайти на машинку:

```bash
docker exec -it <id> bash
```

Где `<id>` - это "CONTAINER ID" при выполнении `docker container list`

Для того чтобы доступиться из parallels до локально поднятого контейнера
(например для проверки в IE11) нужно сначала запустить контейнер на 3000-м порту:

```bash
docker run -p=3000:80 --env-file=/Users/makc-brain/Projects/morda_front/docker/env/testing.txt morda_front
```

Затем поднять прокси с 80-го порта на 3000-ый:

```bash
node docker/proxy.js
```

### Возможные проблемы

При попытке собрать контэйнер вы увидели ошибку "Get https://registry.yandex.net/v2/rasp/ubuntu/trusty/manifests/latest: no basic auth credentials".
Как правило это лечится запуском самого базового образа:

```bash
docker run registry.yandex.net/rasp/ubuntu/trusty
```
