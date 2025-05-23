# Что такое Wall-E

Wall-E – это "управлятор железом". Wall-E автоматизирует полный жизненный цикл сервера, от ввода в экплуатацию до демонтажа. В процессе жизни сервера, Wall-E автоматизирует его передачу между проектами, ремонт, регламентные работы и т.п.

## Место Wall-E в инфрастуктуре Яндекса {#position}
Самое упрощённое преставление об инфраструктуре Яндекса было бы в виде такой простой иерархии:
```
[инфраструктурные сервисы]
            |
        [wall-e]
            |
       [hardware]
```
Инфраструктурные сервисы – это та самая инфраструктура Яндекса, которая помогает быстро запускать новые продукты: Deploy, Nanny, YT, Sandbox, MDB, YDB и другие. Сервисы, которые живут на своём собственном железе, такие как Метрика и Такси, тоже попадают в эту категорию. Продуктовые команды взаимодействуют с инфраструктурными сервисами, а не с Wall-E.

Такая структура понятна и нагляда, но конечно же, не отражает реальность. Инфраструктурные сервисы живут на железе и самостоятельно настраивают его, поэтому нельзя утверждать, что Wall-E польностью изолирует их от железа.

Более того, Wall-E, в отличие от инфраструктурных сервисов, не взаимодействует с железом напрямую: для этого используется набор других сервисов и команд, называемых "инфраструктура датацентров".
```
     [инфраструктурные сервисы]
           /            \
          /              \
         /                \
   [hardware]---[ITDC]---[wall-e]
```
"Инфраструктура датацентров" a.k.a. "ITDC" – это люди и сервисы, которые на самом деле работают с оборудованием: ITDC, EXP, RND, а так же сервисы БОТ, Setup, Eine, IPMI-Proxy.

На самом деле инфрастуктура намного сложнее, и состоит из нескольких слоёв. Если первым слоем была серверная инфрастуктура, то вторым слоем стоит выделить сетевую инфраструктуру:
```
   [инфраструктурные сервисы]
           /         \
          /           \
         /             \
   [network]---[NOC]---[wall-e]
```
С сетью Wall-E тоже не работает напрямую, используя сервисы NOC – службы сетевой инфраструктуры: Racktables и DNS-API.

Третий слой инфраструктуры обслуживает нужды самого Wall-E, это мониторинг и автоматическая дигностика:
```
                   [wall-e]
                    /    \
                   /      \
                  /        \
             [juggler]   [netmon]
              /    \        |
             /      \       |
    [hw-watcher]     +      |
             \      / \     |
              \    /   \    |
               \  /     \   |
           [hardware]  [network]
```
На этой схеме нет инфраструктурных сервисов, чтобы не усложнять связи. На самом деле, Wall-E учитывает ещё и мониторинги, предоставляемые всеми тремя видами инфраструктуры.

{% note info %}

Wall-E является "оркестратором", который управляет этим "оркестром" из людей и сервисов из чётырех разных видов инфраструктуры, получая на выходе работоспособное оборудование для "инфраструктурных сервисов".

{% endnote %}

## Задачи, решаемые Wall-E {#process}
Wall-E интегрирует, оркестрирует и связывает между собой четыре разных уровня инфраструктуры: инфраструктуру сервисов, инфраструктуру датацентров, сетевую инфраструктуру и мониторинг. Всё это делается для того, чтобы обеспечивать автоматизацию жизненного цикла серверного парка.

В первую очередь, новый сервер требуется ввести в эксплуатацию. Для этого Wall-E выбирает серверу имя, прописывает связь сервера с инфрастуктурным сервисом, наливает операционную систему и уведомляет инфраструктуру о готовности сервера к работе.

Дальше сервер живёт своей жизнью, и проходит через различные ситуации:
* сервер может сломаться, и тогда Wall-E его починит
* в Датацентре или в Яндексе может произойти какое-то важное событие, которое затрагивает сервер: учения, отключение электричества, переезд стойки в другой ДЦ и т.п.
* сервер может быть передан другому сервису, списан или демонтирован

Всеми этими процессами Wall-E может управлять для того, чтобы "инфраструктурным сервисам" не приходилось самостоятельно взаимодействовать со всем оркестром из "инфраструктуры датацентра". Это работает и в обратную сторону: "инфраструктура датацентров" и "сетевая инфраструктура" получает от Wall-E такую же поддержку при взаимодействии с "инфраструктурынми сервисами", которые используют Wall-E.

Команды SRE RTC, ITDC и NOC используют Wall-E для сопровождения процессов уровня "всего Яндекса". Часто это глобальные работы, которые затрагивают большинство инфраструктурных сервисов. Среди таких работ:
* переезды серверов и стоек между датацентрами;
* обовление конфигурации и/или замена сетевого оборудования;
* апгрейды и даунгрейды серверов и стоек;
* передача серверов между инфраструктурными сервисами;

Команда SRE RTC работает на стороне Wall-E и часто выступает в роли координатора больших работ между другими инфраструктурными сервисами.

## Из чего состоит инфраструктура {#infrastructure}
Wall-E актвно взаимодействует с четырьмя видами инфраструктуры: "инфраструктурные сервисы", "инфраструктура датацентров", "сетевая инфраструктура" и мониторинг. Что в них входит?

### Инфраструктурные сервисы {#infra}
Под инфраструктурными сервисами мы здесь понимаем такие, которые предоставляют сервисы для продуктовых команд.

#### RTC {#rtc} {#yp} {#nanny}
Самый большой инфраструктурный сервис Яндекса, к которому технически относится и сам Wall-E, это Runtime Cloud – RTC. RTC собрал в себе целую группу сервисов, на которых запускаются новые продукты:
* системы деплоя: Yandex.Deploy, Nanny, Qloud
* системы низкоуровневого управления кластером: iss, skynet, HostManager, DiskManager, GPUManager, и т.д.
* планировщики мощностей: Gencfg, YP
* управление балансировкой трафика для систем деплоя: AWACS

#### Распределённые вычисления {#yt} {#sandbox} {#nirvana}
В инфраструктуре Яндекса есть несколько сервисов для выполнения распределённых вычислений, каждый со своей спецификой и со своим оборудованинем, которой в разной степени проинтегрировано с RTC:
* YT – распределённый map-reduce
* sandbox – распределённое выполнение произвольных вычислительных задач
* nirvana – распределённые вычисления на графах

#### Хранение данных {#mds} {#mdb} {#ydb}
Инфраструктурные сервисы которые позволяют хранить данные, в том числе большие:
* MDS – сервис для хранения произвольных данных в распределённом хранилище
* YDB – распределённая БД с SQL-синтаксисом
* MDB – сервис для централизованного облачного развёртывания популярных баз данных

### Инфраструктура Датацентров {#itdc} {#exp} {#rnd} {#dca}
Люди, которые встречают сервера, когда их привозят с завода, ремонтируют их, провродят регламентные работы и диагностику, называются "ITDC" – инфраструктура датацентров. Инженеры датацентров выполняют "формализованные заявки" на ремонт и диагностику оборудования, проводят апгрейды, следят за состоянием датацентра и т.п. Для нас эти люди представляют что-то вроде первой линии поддержки.

Вторая линия – это EXP, инженеры, которые могут решать более сложные проблемы с диагностикой и ремонтом оборудования. Эти люди могут быть расположены не в датацентре, а например, в московском офисе.

Следующая линия – это RND. Это полностью отдельная служба, которая занимается намного более сложными ситуациями, в частности проектирует наши сервера и стойки, проводит их тестирование до внедрения и сложные исследования проблем в процессе эксплуатации, взаимодействует напрямую с производителями, если того требует проблема.

Люди, которые автоматизируют работу ITDC и EXP, называются DCA – служба автоматизации. Они разрабатывают БОТ, Eine и Setup и IPMI-Proxy.

#### БОТ {#bot}
[БОТ](https://bot.yandex-team.ru/all/) это сложная система, которая используется в логистике, в инфрастуктуре датацентров, в повседневной эксплуатации. В основном это интерфейс в систему складского учёта, которая внутри состоит из OEBS в качестве БД, складского терминала, логистического терминала и ещё всякого разного.

БОТ позволяет работать с предзаказами оборудования - оформление, выдача, приёмка серверов – делаются через этот интерфейс.

БОТ позволяет запросить замену сервера или его деталей – диска, памяти, через интерфейс "формализованных заявок" a.k.a "admin request". Интерфейс настолько прижился, что через него сейчас можно запросить любой ремонт оборудования людьми, в том числе диагностику неизвестных проблем.

#### Einstellung a.k.a. eine {#eine} {#eaas}
[Eine](https://eine.yandex-team.ru/) – это автоматизированная [система для тестирования и диагностики оборудования](https://wiki.yandex-team.ru/dca/services/eine/). Эта система способна загрузить свой образ на полуживой сервер и прогнать на нём тесты, которые покажут большинство имеющихся проблем с оборудованием.

Процедура приёмочных испытаний при получении новых серверов в датацентре называется преднастройкой. Собственно, пользователи называют преднастройкой любой прогон сервера через eine.

Сервер можно тестировать произвольным профилем преднастройки, поэтому другая часть пользователей называет процесс преднастройки "profile" – этот термин используется в Wall-E.

Для Wall-E eine предоставляет режим "Eine as a Service" a.k.a "eaas". В этом режиме eine заводит "формализованные заявки" на любую поломку оборудования, которую она обнаруживает. Из этого режима Wall-E получает сервера, которые способны успешно пройти преднастроечный профиль.

Функционал профилей достаточно гибок, чтобы через с помощью eine можно было установить (задеплоить) на сервер операционную систему, но делать так не рекомендуется, потому что для деплоя есть система setup.

#### Setup {#setup} {#lui}
[Setup](https://setup.yandex-team.ru) – это сервис для [автоматизированной установки операционной системы из образа](https://wiki.yandex-team.ru/dca/services/setup/), по сети. Процесс установки образа называется "наливкой" или "deploy", иногда – "переналивка" и "redeploy".

Когда-то давно Setup умел устанавливать только Linux и назывался LUI – Linux Unattended Installer, так он называется в Wall-E до сих пор. Для установки FreeBSD в те времена существовал FUI. С тех пор Setup научился устаналивать большое количество разных ОС, в т.ч. FreeBSD и Windows.

#### IPMI-Proxy {#ipmi-proxy}
Каждый сервер управляется через IPMI-интерйфейс. Этот интерфейс предоставялется специальным маленьким компьютером внутри сервера, для унификации можно говорить, что этот компьютер называется BMC. У него есть доступ ко всем основным управляющим интерфейсам сервера: ввод-вывод (экран, клавиатура), диски (виртуальный CD-ROM), сеть и т.п.

Из-за такой интимной близости BMC с сервером, доступ к нему ограничен и позволяется только через IPMI-Proxy, которую разрабтывает и поддерживает DCA.

### Сетевая инфрастуктура Яндекса {#noc}
В Яндексе есть служба сетевой инфрастуктуры – NOC, отвечающая за существование сети в датацентрах и офисах Яндекса: наличие, работспособность и корректную настройку сетевого оборудования; проектирование, строительство и эксплуатацию сети, техническую поддержку пользователей. Пользователями является весь Яндекс. Служба NOC разрабатывает внутренний сервис racktables, отдельное подразделение NOC разрабатывает систему управления L3 балансерами L3mgr и систему управления DNS с интерфейсом в виде DNS-API

#### Racktables {#racktables}
Сервис, который предоставляет Wall-E возможность управлять настройками сети для каждого хоста. Этот сервис является мощным инструментом для самой службы NOC, racktables агрегирует информацию о каждом подключении каждого порта в Яндексе, это единственная система, которая технически может определить, в какой порт какого свича подключен какой сервер, и какой именно сетевой картой.

#### ЦК {#cc}
Инструмент для централизованного управления версиями прошивки и конфигов оборудования. Это тоже сильный инструмент, оркестратор, который, среди прочих задач, интегрируется с Wall-E для координации процесса по обновлению прошивок сетевого оборудования.

#### DNS-API {#dns-api}
Инструмент, которым пользуется Wall-E для управления DNS-записями.

### Мониторинг {#monitoring}
Важные части инфраструктуры, на которые Wall-E опирается для того, чтобы понимать, что он делает. Эти сервисы Wall-E использует для собстенных нужд и не предоставляет интеграцию с ними.

#### Juggler
Система сбора событий для мониторинга. Использует собственный сервер pongerd для создания событий активных проверок, которые мониторят доступность серверов по сети.
Имеет агент (juggler-client) для создания "пассивных" проверок, которые присылаются с сервера. Такие проверки используют информацию, предоставляему hw-watcher-ом, а также некоторые собственные диагностические проверки wall-e и инфраструктурных сервисов.

#### hw-watcher
Диагностический инструмент разрабтаываемый на стыке DCA и RND. Умеет определять сбои оборудования и отправлять эту информацию в Wall-E через juggler.
Может работать в режиме, когда он сам запрашивает замену сбойного оборудования через "формализованные заявки" в БОТ-е.

#### netmon
Система мониторинга сетевой связанности. Имеет агентский код практически на каждом сервере Яндекса, агенты обмениваются сетевыми пробами и отправляют результаты на центральный сервер netmon-а.
Центральный сервер вычисляет параметры доступности сети, которые потом Wall-E использует для того, чтобы отличать поломку сервера от сетевых проблем.

## P.S.
Место Wall-E в инфраструктуре Яндекса

![big infrastructure diagram](../_assets/infrastructure.svg)
