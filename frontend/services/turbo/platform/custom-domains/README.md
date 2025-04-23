## Прокси кастомных доменов турбо-страниц

Тут находятся файлы конфигурации nginx, который обеспечивает открытие турбо-страниц на кастомном домене и прохождение letsencrypt challenge для подтверждения владения доменом.

### Схема проксирования

Запрос попадает из внешней сети в L3, который поднимает туннель до веб-сервера nginx. Обработанные запросы, в случае их валидности, проксируются на домен turbopages.org, который ведет на сервисный балансер турбо-страниц, минуя L7 heavy.

Конфигурация прокси находится [тут](https://github.yandex-team.ru/serp/turbo/blob/dev/platform/custom-domains/servers/proxy/nginx.conf), содержит в себе логику отдачи сертификата, обработку проверки доступности с балансера.

При попадании запроса в nginx происходит преобразование url. Из входящего запроса вычисляется ключ документа в SaaS, отделяются внутренние параметры турбо-страниц от параметров, которые нужно прокинуть в ключи. Само преобразование, соглашения и проблемы подробно описаны [тут](https://wiki.yandex-team.ru/users/nox-wave/turbo-proxy/#logikapreobrazovanijavxodjashhegozaprosa).

### Процесс выписки сертификата

Для TLS используются сертификаты [letsencrypt](https://letsencrypt.org/ru/docs/), в качестве клиента используется [certbot](https://certbot.eff.org/docs/).

Для выписывания очередного сертификата необходимо доказать владение доменом или сервером, на который домен ссылается. Эта задача решается отдельным веб-сервером, который умеет отвечать `letsencrypt`. Конфигурацию этого сервера можно найти [тут](https://github.yandex-team.ru/serp/turbo/blob/dev/platform/custom-domains/servers/proxy/nginx.conf).

Единое место отдачи токенов для валидации нужно для упрощения логики доставки токенов на все машины в мультикластерной системе. Вместо этого все инстансы прокси редиректят запрос в одно место, на котором должна храниться вся необходимая информация. Процесс **непосредственно выписывания** сертификата не поребует какой-либо дополнительной раскатки.

Подробное описание процесса валидации владения доменом можно найти [тут](https://wiki.yandex-team.ru/users/nox-wave/turbo-proxy/letsencrypt/) (см. "Немного о проблеме").

#### Выписываем сертификаты в le-acme-challenger

Для того, чтобы выписать сертификат на очередной домен, необходимо на момент выписки сертификата иметь A и AAAA записи целевого домена, указывающие на наш L3. Необходимые IP можно найти, например, в [racktables](https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=9765)
Предположим такой домен у нас есть и это turbo.lenta.ru. Тогда для данного домена надо проделать следующее:
1. Пойти в Yandex.Deploy и найти там stage `le-acme-challenger-production`. Можно так же пройти по [ссылке](https://deploy.yandex-team.ru/project/le-acme-challenger-production).
2. Найти адрес Box'а, на момент написания Readme он называется ChallengerBox ![Пример адреса](https://jing.yandex-team.ru/files/nox-wave/Box_address.png)
3. Подключиться к машине `ssh -6 root@2a02:6b8:c08:7184:0:4448:da4:1`. На ней уже должен быть установлен `certbot`
4. Выписать серт `certbot certonly --webroot -d turbo.lenta.ru -w /var/www` (*)
5. Получившийся сертификат залить в секретницу. Это можно сделать двумя способами:
   - через [интерфейс](https://yav.yandex-team.ru/secret/sec-01dtvrjdvvv17vhfy7jc2g69nd/explore/versions), создав новую версию секрета. Для этого вам потребуется скопировать в буфер обменя сертификат и руками его унести в интерфейс. Так делать не надо.
   - воспользоваться консольной утилитой секретницы. В этом случае мы создаём новую версию примерно так: `ya vault create version sec-01dtvrjdvvv17vhfy7jc2g69nd --oauth=<token> -k "fullchain.pem=<fullchain.pem_content>" "privkey.pem=<privkey.pem_content>"`. Можно загружать секрет как файл, а не строку, но он энкодится в base64, что сломает рантайм. Авторизационный токен [тут](https://nda.ya.ru/3UVsAN). [Документация секретницы](https://vault-api.passport.yandex.net/docs/).

(*) — довольно важно понимать, что сейчас нет никакой возможности донести до certbot уже созданый сертификат и экстендить его. Это значит, что **сертификат необходимо генерировать заново**, включая все домены на которые он уже выписан. Такие домены надо перечислить через `-d` (Например, `-d turbo.lenta.ru -d turbo.rozhdestvenskiy.ru`). Список всех актуальных доменов можно взять [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/turbo/core/utils/custom-domains/custom-domains-list.js).

##### Возможные проблемы
- Отвечаем таймаутом на запросы `certbot`. Это может происходить по причине отсутствия статического IP у сервера, проходящего валидацию. На месте это лечится перезагрузкой `nginx` на **рабочих машинках**. Т.е. надо пойти на машины stage `custom-domain-proxy-prod` и перезагрузить там nginx командой `nginx -s reload`. На постоянной основе это можно починить путём создания домена и внутреннего L3 балансера, который будет статичен.

#### Доставка сертификата
На этом шаге нам понадобится утилита [dctl](https://wiki.yandex-team.ru/deploy/docs/scenarii-ispolzovanija-dctl/). Если у вас есть машина в qyp, то там уже есть все необходимое. Катить будем [custom-domain-proxy-prod](https://deploy.yandex-team.ru/stages/custom-domain-proxy-prod).

Доставляем файл до stage:
1. Скачиваем конфигурацию `ya tool dctl get stage custom-domain-proxy-prod > stage.yml`
2. Открываем в текстовом редакторе и ищем все упоминания **предыдущей** версии секрета (можно взять из [интерфейса секретницы](https://yav.yandex-team.ru/secret/sec-01dtvrjdvvv17vhfy7jc2g69nd/explore/versions)) и заменяем на нужную версию.
3. Поднимаем номер ревизии (revision), пишем описание изменения, если надо (`revision_info: desctiption:`)
4. Отправляем раскатываться `ya tool dctl put stage stage.yml`, если команда выполена успешно, то выкатка произойдёт автоматически.
5. Поглядывать на [сигналы](https://yasm.yandex-team.ru/panel/nox-wave._Oyc4Te/) и статусы в интерфейсе [custom-domain-proxy-prod](https://deploy.yandex-team.ru/stages/custom-domain-proxy-prod).

Подробнее про то, как доставляются секреты описано в пункте про релизный процесс.

### Релизный процесс

Релиз происходит в рамках двух окружений deploy: [le-acme-challenger-production](https://deploy.yandex-team.ru/project/le-acme-challenger-production) и [custom-domain-proxy-prod](https://deploy.yandex-team.ru/project/custom-domain-proxy-prod). Релизить сразу оба, обычно, не требуется.

**Важно!** Использовать GUI для релизов **не стоит**! В текущий момент не все поля конфигурации доступны в GUI Yandex.Deploy и их необходимо править руками в `.yaml` файле. Если вы попытаетесь изменить конфигурацию в GUI и раскатить ее, то **все изменения сделанные вне интерфейса будут стерты**. Для релизов необходимо использовать утилиту [dctl](https://wiki.yandex-team.ru/deploy/docs/scenarii-ispolzovanija-dctl/).

**Важно!** Хранить, полученный в результате работы с `dctl`, конфиг `stage` в системе хранения версий **нельзя**. На момент написания ридми, важные данные про секреты (TVM тикеты, в частности) пишутся прям в конфиг. Если положить в репозиторий — за вами приедет воронок СИБа.

Полного примера конфига в формате `.yaml` не имеется, документации (человекочитаемой) по полям тоже. Если потребуется добавить что-то новое или посмотреть возможные значения, то придется читать [protobuf](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/stage.proto?rev=4996458#L26). Примеры, возможно, получится найти в документации к самому [деплою](https://wiki.yandex-team.ru/deploy/)

#### Как собрать docker контейнер с прокси

1. Авторизоваться в реестре по [инструкции](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization)
2. Убедится, что есть доступы к префиску `turbopages` или к конкретному репозиторию (например, `turbopages/custom-domain-proxy`). Посмотреть можно на [IDM](https://idm.yandex-team.ru/#main=roles,sort-by=-updated,f-status=all,f-is-expanded=true,f-system=docker,f-role=docker) (доступы раздавались на Рантайм Турбо-страниц, так что должны быть
3. Перейти в директорию `platform/custom-domains`).
4. Запустить сборку `npm run build:[proxy|challenger] -- --tag <your tag>`. Наример, для сборки proxy с версией `0.0.20` надо выполнить следующее `npm run build:proxy 0.0.20`. В результате локально будет собран образ `registry.yandex.net/turbopages/custom-domain-proxy:0.0.20`
5. Запушить образ в репозиторий `docker push registry.yandex.net/turbopages/custom-domain-proxy:0.0.20`

#### Как доставить новую версию контейнера до деплоя

Тут показывается как выглядят действия при простейшем релизе. Все аналогично действиям из пункта про доставку сертификата

1. На своей виртуальной машине `ya tool dctl get stage custom-domain-proxy-prod > stage.yml`
2. Находим внутри `CustomDomainDeployUnit` свойство `images_for_boxes`, в котором декларативно описаны контейнеры для всех Box в нашем stage. На текущий момент Box один — `CustomDomainBox` ![Поле для изменения](https://jing.yandex-team.ru/files/nox-wave/up_tag_custom_domains.jpg)
3. Обновляем информацию о нужном контейнере. Меняем `tag` на нужный нам
4. Необязательно, но желательно: меняем `revision` и `revision_info`
5. Заливаем в deploy `ya tool dctl put stage stage.yml`

### Скрипты

В папочке `custom-domains/scripts` есть скрипты, которые могут пригодится (не сказать, что я их сильно проработал...)

**build-nginx** — скачивает все необходимое для локальной сборки nginx + njs из исходников, конфигурирует и запускает компиляцию. Итоговый бинарь кладется в /usr/local/bin

**create_certificate_for_domain** — позволяет создать самоподписный сертификат для локальной разработки

**configure** — копирует js файлы и конфиги в /etc/nginx для локального запуска

**build-docker** — используется командой `npm run build:...`

### Как развернуть локально
TODO

### Как выписать самоподписный сертификат для разработки
TODO
