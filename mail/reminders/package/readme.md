# Введение
Данный пакет предназначен для запуска в QLoud в совершенно автоматическом режиме, однако может возникнуть потребность запустить этот образ для отладки на локальной машине или на виртуальной машине разработчика. Помимо этого, желательно разобраться с тем, как именно работает образ и чего он ждет извне.

# Переменные окружения 
Образ ожидает нескольких переменных, передаваемых извне. Первая называется PROGRAMNAME и может принимать два значения - либо api, либо worker. Попытка передать какое-либо другое значение приведет к ошибке. Несложно заметить, что эта переменная всплывает в supervisor/reminders.conf, и передается в качестве аргумента при запуске программы.

Вторая переменная называется QLOUD_ENVIRONMENT и называется она так потому, что она проставляется QLoud автоматически. Используется она в entrypoint.sh в следующей команде:

> echo $QLOUD_ENVIRONMENT > /etc/yandex/environment.type

А приложение уже считывает эту переменную из файла. 

# Способ запуска

Для запуска нужно зайти в каталог mail/reminders/docker-compose и там запустить run.sh. Почему это в отдельном каталоге? Потому что в данном каталоге package располагается только то, что реально необходимо для сборки образа, пригодного для установки к Qloud. А вот все, что относится к запуску на локальной машине разработчика, это в отдельном каталоге. Зачем понадобился Docker Compose? А затем, что нам нужна поддержка TVM, и для этого отдельным контейнером мы запускаем tvmtool демона, к которому и будет обращаться наш образ. 

Почему бы не включить в наш образ tvmtool демон, спросит пытливый читатель? А затем, что этот демон есть в Qloud, и его как раз включать в образ не надо. Поэтому для отладки на локальных машинах нужно создать свой образ. Детали окружения docker compose описаны в mail/reminders/docker-compose/readme.md.

# Содержимое основного образа

Образ Docker здесь содержит следующие вещи:

* Настройки супервизора, который при необходимости перезапускает приложение, если оно вдруг рухнет.
* Настройки ротации логов, это крайне важно, поскольку иначе логи не будут уезжать в YT, а они должны. Кроме того, логи должны ротироваться и помещаться в архивы раз в сутки.
* Настройки nginx. 
* Настройки monrun для проведения пассивных  проверок в juggler.

Кто-то может задаться вопросом, зачем нужен nginx? А он нужен для взаимодействия  с L3/L7 балансерами. Он отвечает за следующие вещи:

* Поддержку http и https. При этом образ построен достаточно хитро. Если сертификата нет, то он обслуживает чисто 80-й порт. Если же есть файл сертификата из секретницы QLoud, то он будет использовать его. Файл должен быть прописан по пути /etc/nginx/ssl/reminders.pem, и содержать в себе как публичную часть, так и приватный ключ. 
* Унификацию ручек. Смотрите, наше приложение отдает ответы по разным портам. Главный порт, по которому происходит взаимодействие, это 22266. Однако рукоятки админки по пингу Mongo располагаются по ручкам 22260 для api  и 22261 для worker (такое разделение осталось со времен, когда оба компонента запускались на одной виртуальной машинке). Все это будет доступно по 80 и 443 портам по ручкам /ping, /ping-mongo, /ping-alive-apps.

# Проверки monrun

В базовом образе мы получаем monrun и juggler клиент. И возможность запускать набор проверок. Здесь проверки можно разделить на три типа:

* Базовые проверки, необходимые для любого образа. Это cron, META, unispace и load_average, которые я не буду здесь особо освещать. Скажу лишь, что осбенно важен unispace, чтобы не прозевать момент, когда место в контейнере будет близко к исчерпанию.
* Специфичные проверки, основанные на том, что monrun обращается к той или иной ручке приложения, и если получает ответ не 200, то это повод для тревоги.
* Специфичные проверки, основанные на анализе nginx логов. 

Так, что за ручки дергает monrun?

* ping. Ну здесь все очевидно, это базовая ручка, которая должна быть доступна всегда после старта приложения. Кстати, эта проверка единственная, которой следует быть активной, т.е. кто-то должен дергать извне эту ручку, а не просто само приложение оповещать об этом.
* ping-mongo - проводит базовую проверку базы mongo, а нет ли там чего подозрительного, может, что из реплик отвалилось, или база в принципе недоступна.
* ping-alive-apps - самая нетривиальная проверка. Для api она всегда возвращает ОК, поскольку для api она смысла не имеет. А вот для воркеров еще как имеет. Она проверяет посредством обращения в zookeeper, а не возникло ли расхождения по версиям - т.е. нет ли в наличии сейчас в указанной группе воркеров сразу нескольких версий? Если есть, то ручка возвращает 500 и описание в формате json, какие экземпляры какой версии имеются. Это особенно критично для QLoud, где есть риск возрождения старых тачек воркеров.

Что за анализ логов проводит monrun?

* Анализ на коды 4xx, 5xx, если они недавно появлялись. Отдельно выделена проверка на код 499, поскольку остальные коды 4хх могут считаться валидными, и в таком случае проверку на них стоит притушить.
* Анализ на превышение времени ответа приложения, если он больше одной секунды, то это повод забить тревогу.

Для анализа логов nginx специально пишет лог /var/log/nginx/reminders.access.tskv.log, который monrun парсит с использованием специальной утилиты timetail, проверяя только последние 5 минут в логе, а не весь лог.

# Оптимизация по слоям

См. раздел с таким же названием в mail/calendar/package/readme.md - там детальное обоснование, почему сделано именно так.