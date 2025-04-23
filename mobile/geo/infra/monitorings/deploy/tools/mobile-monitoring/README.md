## Скрипты для сбора данных для мониториноов.

Каждый из *.sh скриптов запускают один из *.ts скриптов. <br />
*.ts скрипты забирают данные из ClickHouse или AppMetrica и из них вычисляют данные для сигналов. <br />
Данные сигналов складываются в файлы в папке $MOBILE_MONITORING_SIGNALS_DIR <br />
Из этих файлов данные для сигналов забирает Голован.

---

Отладка скриптов для сбора данных:
* Переходим в папку [monitorings/deploy](../../) 
* Переключаемся на node нужной версии `nvm use` Если напишет, что nvm не установлен, то ставим nvm. https://github.com/nvm-sh/nvm#install--update-script
* Устанавливаем зависимости `npm ci`
* Билдим исходники - `make build`
* Запускаем нужный скрипт. Например `node out/tools/mobile-monitoring/get-mobile-crash-data.js`
  
Переменные окружения, необходимые для разработки.
Добавляем переменные окружения в .bashrc или .zshrc.
* `MOBILE_MONITORING_SIGNALS_DIR` - Путь до папки, куда сохраняются результаты сбора мониторингов. 
* `MOBILE_MONITORING_CLICKHOUSE_USER` и `MOBILE_MONITORING_CLICKHOUSE_PASSWORD` - Пользователь и пароль, с которым скрипт будет ходить в ClickHouse
* `HAMSTER_YT_TOKEN` - Токен для похода в YT https://oauth.yt.yandex.net/

**После выполнения скрипта в MOBILE_MONITORING_SIGNALS_DIR появятся файлики с значениями сигнала.**

Если были добавлены новые скрипты, то необходимо сделать следующее:
* Добавляем `echo 0 > $MOBILE_MONITORING_SIGNALS_DIR/signal_name` в [init.sh](./init.sh) <br /> Создаем файл сигнала с изначальным значением, чтобы оно всегда было в системе.
* Добавляем или модифицируем существующий cron скрипт. <br /> 
Например, если был добавлен новый сигнал технического события, то достаточно просто добавить зануление в cron-maps-tech-events.sh. <br /> 
Зануление необходимо для того, чтобы сбросить предыдущее значение, если скрипт по какой-то причине упал (отработал с ошибкой node скрипт или наткнулись на yt-lock).
* Если был добавлен новый сигнал, который не относится никак к предыдущим, то необходимо написать новый cron скрипт по аналогии с другими и добавить его в cronтаб [.config/cron/mobile-crash-data.conf](../../.config/cron/mobile-crash-data.conf)
* Добавляем в папку [../../.config/checks](../../.config/checks) shell скриптик для нового сигнала. <br /> 
Задача скрипта вывести значение файла сигнала. Имя файла задается в формате signal_name_axxx.sh. Именно эти скрипты будет запускать Голован для сбора сигналов.

---

##ClickHouse##
Некоторые скрипты берут данные из ClickHouse. Примеры скриптов можно увидеть ((https://github.yandex-team.ru/maps/mobmaps-proxy-api/blob/master/tools/mobile-monitoring/get-maps-tech-events.ts#L12 тут)) и ((https://wiki.yandex-team.ru/maps/mobile/dev/common/monitoringi/ тут)).

Описание таблиц с событиями аппметрики.
((https://wiki.yandex-team.ru/jandexmetrika/data/appmetricatables/eventsall/))

---

##yt_lock##
Для того, чтоб только один инстанс в одно время собирал мониторинги есть специальные симафоры. <br />
`yt_lock.py <path_ya_lock_file> "<comand>" --proxy locke.yt.yandex.net` <br />
yt_lock.py - утилита для распределённой блокировки на основе YT <br />
https://wiki.yandex-team.ru/avia/dev/distributed-yt-locks/

Чтобы дебажить yt_lock, нужен доступ к папке в YT, в которой будет создаваться блокировка. <br />
У Хамстера есть доступ в папку `//home/maps_mobile/` на проксе `locke`. Там же лежат билдкаунтеры для сборок. <br />
https://yt.yandex-team.ru/locke/navigation?contentMode=resources&path=//home/maps_mobile

Если нужен новый lock, нужно его создать. Вызвать блокировку с параметром `--create-lock` <br />
`yt_lock.py <path_ya_lock_file> "<comand>" --proxy locke.yt.yandex.net --create-lock`

Локально yt_lock можно запустить по пути в аркадии 
`/yt/python/yt/tools/bin/lock_make/yt_lock`
