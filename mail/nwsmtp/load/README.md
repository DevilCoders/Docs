## Нагрузочное тестирование

### Стенд
**smtp-loadtest1p.mail.yandex.net**
Поддерживает сервисы:
**nwsmtp**
Рабочий каталог: /etc/nwsmtp
файлы конфигурации для нагрузки:
* stress-mxback-out.yml
* stress-mxback.yml
* stress-mxfront.yml
* stress-smtp.yml
**fastsrv** 
**postfix**
**smtpgate**

[Jenkins](https://jenkins-load.yandex-team.ru/job/nwsmtp)-джоба для запуска нагрузочных тестов.

### Что тестируем
* Отправку сообщений 
* Отправку сообщений в рамках сессии
* Отправку сообщений с временной задержкой

### Пушка
Пушки: [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/mail/nwsmtp/load/tools)
* smtp-no-sessions.jmx - для простой стрельбы;
* smtp-sessions.jmx - для стрельбы с сессиями;
* smtp-delayed.jmx - для стрельбы с задержками.

### Танки
fobos.tanks.yandex.net
mars.tanks.yandex.net

### Параметры стрельбы, которые можно настроить через Jenkins задачу:
* ***TASK*** - Тикет в StarTrek, с которым будет ассоциирован нагрузочный тест;
* ***NOTIFY*** - список пользовотелей, для оповещений;
* ***COMMENT*** - комментарий к тесту;
* ***HOST*** - цель нагрузочного теста;
* ***PORT*** - порт, который слушает исследуемый сервис;
* ***SSL*** - критерий шифрования трафика;
* ***THREADS*** - число потоков генератора нагрузки, которое может быть задействовано во время теста; 
* ***START*** - число сообщениий после создания всех тредов;
* ***END*** - максимальное число сообщений;
* ***RUMPUP*** - параметр длительности теста;
* ***TIME*** - ещё один параметр длительности теста;
* ***AMMO*** - файл с письмами в формате танковой аммуниции.. Располагается на каждом из допустимых танков;
* ***USERS*** - файл с параметрами авторизациии и метаданными для отправки писем;
* ***LOCK_HOSTS*** - хосты, взаимодействие с которыми со стороны танка будет зарезервировано;
* ***CLEAN_MAILBOXES*** - очистить почтовые ящики перед тестом;
* ***AUTH*** - проводить ли авторизацию пользователей перед отправкой писем;
* ***CTO*** - таймаут для соединения;
* ***RTO*** - таймаут для запроса;
* ***SESSIONS*** - строка с указанием параметров сессии для сессионых стрельб;
* ***COMPONENT*** - компонент стрельбы; 
* ***CONFIG*** - базовый конфиг сервиса для нагрузочного теста. Должен быть расположен на се##рвере цели;
* ***NW_OUT*** - тестировать сервис nwsmtp-out;
* ***AUTOSTOP*** - критерии автоматической остановки стрельбы;
* ***UPSTREAM_BUILD*** - 
* ***DELAY*** - задержка при отправке сообщений в рамках одного треда при стрельбе с задержкой; 
* ***JMX*** - генератор jMeter, который будет использоваться для нагрузки
* ***DBHOST*** - хост базы данных для скрипта очистки почтовых ящиков;
* ***DBPASS*** - пароль для скрипта очистки почтовых ящиков.

### Вспомогательные скрипты
* clean_inbox.py - очищает почтовые ящики, посредством обработки таблиц **mail.deleted_box** и **mail.messages**;
* sessions.py - формирует файл sessions для сессионных стрельб на основе параметра ***SESSIONS***;
* nw_av_stat.py - собирает дополнителную статистику мониторинга.

### Стрельбы
Запуск задачи nwsmtp в Jenkins выполняется скрипт **nwsmtp_job.sh**, который формирует дополнительные параметры на основе указанных в Jenkins и переменных окружения, а также обращается к цели для получения версий ***NWSMTP***, ***FASTSRV*** и ***POSTFIX***. Если установлен флаг ***CLEAN_MAILBOXES***, то перед нагрузкой производитсяочищается таблицы **mail.deleted_box** и **mail.messages** через выполнение скрипта **clean_inbox.py**. Также задается файл настроек тестируемого сервиса через включение в качестве базового файла, указанного в параметре ***CONFIG***, а сам сервис перезапускается. При этом файл настроек должен располагаться на хосте цели. Далее через tankapi на свободный танк передаются необходимые файлы и параметры теста и запускается указанный генератор нагрузки.

Генератор нагрузки определяет порядок и параметры подключения, устанавливает соединение с целью, отправляет приветствие и проходит авторизацию для каждого пользователя (опционально), исходя из заданных условий стрельбы. В случае успешного прохождения этих шагов производится отправка сообщения или сообщений в соответсвии с выбранным генератором нагрузки. Данные для нагрузки последовательно и циклично выбираются из файлов ***USERS*** и ***AMMO***. В качестве ***AMMO*** передается только путь до файла. Сами файлы с телами сообщений, ввиду их большого размера, расположены на танках fobos.tanks.yandex.net и mars.tanks.yandex.net.

Длительность стрельбы определяется суммарным показателем параметров ***RUMPUP*** и ***TIME***, причем сначала за время ***RUMPUP*** нагрузка возрастает от 1 rps до параметра ***START***, после за время ***TIME*** нагрузка возрастает от ***START*** до ***END***, таким образом характер стрельбы (линейная или постоянная) можно задавать через эти параметры. Рекомендуется задавать достаточно большие значения для ***START*** (от 30) и ***END*** (от 100 и выше) для того, чтобы треды при создании имели содержание. Иначе стрельба может зависнуть.

Дополнительно, в момент запуска танка, на сервер цели передается и запускается на ней скрипт **nw_av_stat.py**, что позволяет собрать больше данных о поведении сервиса под нагрузкой.

#### Особые случаи стрельб
* При стрельбе с шиифрованием в параметре ***CONFIG*** следует указать ```base: /etc/nwsmtp/stress-smtp.yml```, поскольку только с этим конфигом сервис слушает 465 порт, который должен быть указать в параметре ***PORT***, для шифрованных соединений.
* При стрельбе с авторизациией следует отметить параметр ***AUTH*** и в параметре ***USERS*** выбрать файл пользовательских данных ```users.auth.real.csv``` или ```users.auth.pg.csv```. Авторизация на сервисе возможно только при ssl шифровании.
* При стрельбе с сессиям следует учесть, что сессия возможна только при авторизации, а значит и шифровании соединения. Поэтому для сессионной стрельбы следует установить JMX=smtp-sessions.jmx, PORT=465, SSL=true, CONFIG=```base: /etc/nwsmtp/stress-smtp.yml```, AUTH, в SESSIONS указать тип, длительность и число сессий разделенные запятыми (как показано в образце), в USERS указать файл данных пригодный для авторизации.
