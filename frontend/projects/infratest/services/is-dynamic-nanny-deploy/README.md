# Is it dynamic nanny deploy?

Сервис, который отвечает на вопрос "деплой в nanny обновит только [динамические ресурсы](https://wiki.yandex-team.ru/runtime-cloud/nanny/howto-manage-service/#dynamic-resources)?".
В самой nanny таких инструментов нет и не планируется.

Предназначен для использования на nanny dashboard для остановки деплоя, если будут изменены не только динамические ресурсы.
Такие изменения приводят к перезапуску инстанса и при использовании operating_degrade_level=1 (как часто делается для деплоя динамических ресурсов) может привести к даунтайму сервиса.

Исходная проблема описана в https://st.yandex-team.ru/FEI-17614.

Для каждого nanny-сервиса в alemate taskgroup строится diff между active и head снепшотами.
Если разница только в файлах, которые помечены флагом `Is dynamic`, то такое изменение считается динамическим и is dynamic deploy ответит кодом 200, иначе - 400.

## Использование

В [мета-рецепте nanny](https://wiki.yandex-team.ru/runtime-cloud/nanny/dashboards/metarecipes-ui/) добавить кубик http_request с адресом `http://is-dynamic-deploy.si.yandex-team.ru/`.

![Пример использования](./doc-imgs/cubic.png)

### Что делать, если кубик красный

Выбери один вариантов ниже.

#### Спросить дежурного

[Дежурный renderer](https://abc.yandex-team.ru/services/reportrenderer/duty/).

#### Посмотреть логи

Логи приложения: https://deploy.yandex-team.ru/stages/is-dynamic-deploy-main/logs?deploy-unit=main.

На красном кубике кликаем `Show alemate task status`.

![Красный кубик](./doc-imgs/red-cubic.png)

В появившемся окне кликаем на "View in alemate UI".

![Подробности](./doc-imgs/cubic-details.png)

В alemate ui будет видно сообщение об ошибке, например:
```
Result: FAIL:
Got HTTP code 400, code 2xx expected. Reply was: Specified deploy can cause container stop/start in services renderer_load_test. See https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/services/is-dynamic-nanny-deploy for debug instructions. Debug logs: https://deploy.yandex-team.ru/stages/is-dynamic-deploy-main/logs?deploy-unit=main&query=message%3D%22deploy-0204554247%22
```

Перейти по ссылке из сообщения.
Обычно по логам можно понять, что же нединамического было изменено:

![Логи в deploy](./doc-imgs/deploy-logs.png)

Если этого недостаточно, то в одном из сообщений будет diff двух состояний: active (текущее состояние) и head (то, в которое хотим перевести сервисы).

![Diff двух состояний](./doc-imgs/diff.png)

Далее я предполагаю, что в дашборде есть два рецепта: для "динамических" изменений, когда можно катить с высоким [operating degrade level](https://wiki.yandex-team.ru/runtime-cloud/nanny/alemate/yaml-recipes/#operating-degrade-level-desc) вплоть до 1 и для всех остальных изменений с низким operating degrade level.

Если понятно, что изменения лишние (такое бывает, например, если остановили битый релиз, но не откатили head или вместе со своими изменениями покатили чужие), то нужно:
* текущий деплой нужно остановить
* если принято решение "качу с этими изменениями", то запустить деплой безопасным рецептом
* иначе привести сервисы в то состояние, которое нужно выкатить

Если понятно, что изменения лишние, но они не должны приводить к остановке процессов в контейнере, переходи к пункту "проверить, будет ли остановка процессов".

Если непонятно, что за изменение, смотри раздел "известные проблемы".

Если лишних изменений нет, но is-dynamic-deploy отвечает не 200 кодом, то создай тикет https://st.yandex-team.ru/createTicket?queue=INFRADUTY&_form=17756.
* инструмент - "инструмента или сервиса в списке нет"
* заголовок - "Проблемы с is-dynamic-deploy"
* текст обращения - добавить ссылку на деплой в nanny и логи; описать, что ожидалось и что происходило на деле.

После создания тикета поставить ему "ABC Service": "Report Renderer Development".

В течение 30 минут дежурный renderer посмотрит на сообщение.

Если сервис блокирует релиз в прод, то написать в личку дежурному renderer, если не отвечает - позвонить по телефону.

#### Проверить, будет ли остановка процессов

Для каждого из nanny-сервисов, участвующих в деплое:
* перевести один инстанс в active
  ![Список инстансов](./doc-imgs/instances.png)
  ![Активировать инстанс](./doc-imgs/activate-instance.png)
* убедиться, что инстанс при активации проходит состояние "DYNAMIC_RESOURCE_EXECUTION"
  ![Нужный статус](./doc-imgs/dynamic-resource-execution.png)

Если это так, то всё в порядке - такое изменение можно прокатывать с высоким operating degrade level.
Кубик можно пропустить, нажав done:
![Done](./doc-imgs/done.png)
![I know what I'm doing](./doc-imgs/i-know-what-i-am-doing.png)

В противном случае активация этого снепшота будет приводить к остановке процессов в контейнере и прокатывать нужно с низким operating degrade level.

### Известные проблемы

Иногда при коммите тикета в nanny-сервис, когда должен был измениться только один или несколько ресурсов, nanny вносит свои изменения: https://st.yandex-team.ru/SWAT-7685.
Особенно часто так добавляются новые дефолты в nanny.
Обычно в таких случаях процессы в контейнерах не останавливаются, поэтому достаточно убедиться в этом на одном из инстансов и пропустить кубик с запросом к is-dynamic-deploy.

## Разработка

### Как собрать?

```sh
npm i
npm run build
```

### Как запустить?

```sh
npm start -- -p 3000
```

### Как разрабатывать?

```sh
npm run watch
```

### Как собрать Docker-образ?

```sh
npm run docker-build
```

При сборке в QYP могут быть проблемы с ipv6 внутри контейнера, можно пробросить сеть с хоста:
```sh
BUILD_ARG="--network host" npm run docker-build
```

### Как запустить Docker-образ?

```sh
npm run docker-build
RUN_ARG="-p 3000:80 -e NANNY_TOKEN=<NANNY_TOKEN>" npm run docker-run
curl http://localhost:3000
```
  
Токен nanny можно получить по адресу https://nanny.yandex-team.ru/ui/#/oauth/.

### Как обновить образ?

Влить изменения в dev.
Будет автоматически выпущена новая версия.
После этого в trunk выполнить

```sh
npm run docker-publish
```
  
Зайти на сервис https://deploy.yandex-team.ru/stage/is-dynamic-deploy-main и обновить docker-образ для сервиса.

### Где запускается проект

https://deploy.yandex-team.ru/stage/is-dynamic-deploy-main

Поддержкой сервиса занимается команда [is-dynamic-deploy](https://abc.yandex-team.ru/services/is-dynamic-deploy/)

### Как залить обновление образа

![how-release](./doc-imgs/how-release.png)
Убедиться что первые 3 таба, отмеченные стрелочками, выбраны правильно.
Нажать Edit под 4 стрелкой.
![how-release-2](./doc-imgs/how-release-2.png)
Отредактировать Docker-тег и потом нажимать релизы.

[Ссылка на место из скриншота](https://yd.yandex-team.ru/stages/is-dynamic-deploy-main/config/du-main/box-app#resources)

### Как потестировать

#### Prod

В сервисе [test-is-dynamic-deploy](https://nanny.yandex-team.ru/ui/#/services/catalog/test-is-dynamic-deploy) изменить static file или dynamic file.

Начать новый деплой рецептом prod на дашборде [test-is-dynamic-deploy](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/test-is-dynamic-deploy).

#### Локально запущенный сервис

В сервисе [test-is-dynamic-deploy](https://nanny.yandex-team.ru/ui/#/services/catalog/test-is-dynamic-deploy) изменить static file или dynamic file.

Запустить сервис на публично доступном адресе (например, в QYP) или пробросить порт при помощи [tunneler](https://doc.yandex-team.ru/si-infra/tunneler/usage.html#iz-shell).

В рецепте [local](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/test-is-dynamic-deploy/recipes/catalog/local) прописать правильный адрес в http_request.

Начать новый деплой рецептом local на дашборде [test-is-dynamic-deploy](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/test-is-dynamic-deploy).

### Как обновить алерты

```sh
npm run upload-alerts
```

Алерты не обновляются автоматически.

[Дока по алертам](./alerts.md)

### Как игнорить изменение дефолтов няни

(Только если убедились что эти изменения не мешают динамическому обновлению ресурсов)

* Найти [правильные логи](https://deploy.yandex-team.ru/stages/is-dynamic-deploy-main/logs?deploy-unit=main&query=message%3D%22Fields%20that%20are%20not%20resources%22)
* Скопировать context.msg, далее в [папку со скриптом](https://a.yandex-team.ru/arc_vcs/junk/maxeljkin/is-dynamic-deploy-defaults)
* Вставить скопированное в diff.txt, запустить `node extract_diffs.js`
* Скопировать вывод, он пригодится для обновления defaults
* [Зайти в деплой](https://yd.yandex-team.ru/stages/is-dynamic-deploy-main/config/du-main#disks)
* ![how-release-config](./doc-imgs/how-release-config.png)
* Убедиться что первые 3 таба, отмеченные стрелочками, выбраны правильно.
* Нажать Edit под 4 стрелкой.
* В новой странице найти блок со Static resources
* ![how-release-config-2](./doc-imgs/how-release-config-2.png)
* Добавить изменения
* Дальше катить как после обновления образа

