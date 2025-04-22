# Полезные чаты

Также см. [список дежурств](duty.md).

Рекомендации на что подписываться в первую очередь: [{#T}](sources-to-read.md)

## Директ { #direct }

### direct-dev-announces (канал) { #direct-dev-announces }

Инвайт-ссылка: <https://t.me/joinchat/AAAAAEdsh-Tn69GPfKNvmw>  
Важные анонсы для всей разработки Директа.   
Права постить сообщения есть у: [Саши](https://staff.yandex-team.ru/ppalex), [Юры](https://staff.yandex-team.ru/yukaba), [Макса](https://staff.yandex-team.ru/maxlog), [Марины](https://staff.yandex-team.ru/mspirit)

### direct-dev-talks { #direct-dev-talks }

Инвайт-ссылка: <https://t.me/joinchat/BV5nDD4xzjnRu3ImGsemxw>  
Общение разработки Директа.  
В разумных околорабочих пределах можно писать все и всегда. У многих может быть замьючен.  
Если репортишь срочную проблему — пиши лучше в тревожный чат.  
Аналогичный чат в Ямбе: <https://yamb.yandex-team.ru/#/join/67836bea-6458-4e68-81cb-0bba55723a6b>, скорее неживой

### Тревожный чат / "Дежурство в Директе" { #direct-prod-problems } 
Он же "чат с котом"  
Инвайт-ссылка: <{{chat-direct-duty}}>  
Координация срочных задач и проблем в продакшене Директа  
Если видишь серьезную проблему в продакшене — пиши в этот чат (если могут быть задеты соседние сервисы, то продублируй в [Поломки Рекламы](#adv-services))

Для привлечения внимания дежурных к срочной проблеме в продакшене рекомендуется использовать команду `/duty_call`.

NB: duty_call — это срочные призывы, когда надо немедленно начинать разбираться; нужен для того чтобы формализовать процесс и собираться статистику по времени реакции. Например "сегодня" это не тот уровень срочности. Абьюзить duty_call не надо. Инфраструктурные вопросы это скорее в сторону админского чата. В чате "Дежурство в Директе" срочные проблемы аффектящие пользователей.


### direct-incidents { #direct-incidents }
Канал в слаке <{{incidents-channel}}> рабочей группы по инцидентам.
Обсуждаем подготовку к еженедельным встречам.

### Direct.Admin.Chat { #direct-admin-chat }

Он же "админский чат"  
В Телеграме (основной чат): <{{chat-direct-admin}}>  
В Ямбе (на всякий случай про запас): <https://q.yandex-team.ru/#/join/406230db-96c6-46ad-9668-24951aace65e>   
Писать: запросы на выкладку, срочные вопросы про продакшен и т.п. Релевантные конструктивные обсуждения уместны в разумных количествах. Ночью по Москве (21-10чч) несрочное лучше не писать — или сделать тикет, или написать позже.

Подписываться "на всякий случай про запас" не стоит. Если не расследуешь проблемы с продашкеном — наверное, этот чат тебе не нужен.

### Чат direct-app-duty { #direct-app-duty }

Обсуждение вопросов по app-duty дежурствам (дежурство по продакшену)

Инвайт-ссылка:  есть на wiki-странице app-duty. Когда присоединишься к ротации дежурств, тебе все покажут.  
Подписываются дежурные по продакшену.  
Во время дежурства чат ожидается незамьюченным, вне дежурства можно мьютить.

Тем, кто не участвует в дежурстве, подписываться не надо. Вопросы можно писать в Direct.Admin.Chat, острые проблемы в продакшене — в Тревожный чат


### Директовский аварийный чатик, УСТАРЕЛ { #deprecated-1 }

Устарел. Пользуйтесь [Тревожным чатом](#direct-prod-problems) или [звоните дежурному app-duty](#app-duty-phone).

Инвайт-ссылка: <https://telegram.me/joinchat/AIDJtQGJH_Ic0rz7yJkKIw>

Раньше был про аварии Директа в нерабочее время.

### direct-release { #direct-release }

Инвайт-ссылка: <{{chat-direct-release}}>  
Координация тестирования релизов

### direct-releases-duty { #direct-releases-duty }
Инвайт ссылка: <{{chat-release-duty}}>  
Чат для дежурных по релизам.

### direct-perl-regression { #direct-perl-regression }
Канал в слаке про регрессию в перловых релизах: <https://yndx-ad-tech.slack.com/archives/C01HPNQDNSZ>

После внедрения новых дежуртсв по релизам+ТС канал умер в пользу чата [{#T}](#direct-releases-duty), однако его история может быть полезной.

### Storybook Test Support { #storybook-support }
Чат поддержки про написание storybook-тестов.  
<https://t.me/joinchat/4EnOqu8kP7QwNmZi>

### DNA Test Duty  { #dna-test-duty }
Чат поддержки по автотестам в DNA 
Есть дежурный, который обладает наибольшим контекстом того, что сейчас стабильно и какие существуют проблемы — можно сообщить или получить ок на мерж
<https://t.me/joinchat/RgI69t6JcVJ5AORs>

### Direct No Architecture { #direct-no-architecture }
Общий чат фронтенда
Здесь можно спросить все, что касается фронтенда Директа: от переменных до селеноидов 
Еще можно делать анонсы, которые затрагивают привычный воркфлоу работы
Вам подскажут или отправят в нужный чатик
<https://t.me/joinchat/TrHQwTqlZ4pmM2Y6>


### Приложенческие релизные чаты { #app-release }

Экспериментальные чаты с авто-уведомлениями про релизы отдельных приложений.

Предположительно подходящий режим использования: замьютить и запинить.
Или замьютить, вынести в отдельный каталог и запинить там.

Предложения, что еще надо писать в эти чаты, приносите lena-san@

- canvas: <https://t.me/joinchat/BV5nDFTa-Onnz-lHEuZKlQ>
- java-api5: <https://t.me/joinchat/BV5nDEwIXXzALuPwliZ1tg>
- java-intapi: <https://t.me/joinchat/BV5nDE2n9FGguZmaju3urA>
- java-jobs: <https://t.me/joinchat/BV5nDE4LChmFPhLEuhUxcw>
- java-logviewer: <https://t.me/joinchat/BV5nDEtuO_MPZrXudaZGlA>
- java-web: <https://t.me/joinchat/BV5nDEt7OCqESmukGzwVug>
- oneshot: <https://t.me/joinchat/BV5nDEeIak03DRLJmyZA2g>


### Дизайн-ревью { #design-review }

Инвайт-ссылка: <https://t.me/joinchat/BV5nDBawrE0E5VRIz9tXYg>  
Обсуждения в рамках дизайн-ревью в Директе


### Чат про внутреннюю документацию Директа { #docs }

Инвайт: <https://t.me/joinchat/CjerUhlubC3jVqFbipRVEQ>  
Обсуждение внутренней документации Директа


### Direct API { #direct-api }

Инвайт-ссылка: <https://t.me/joinchat/AAAAAADK2lFHgHU9ZKSEHA>  
Чат группы разработки API к Директу для обсуждения текущих вопросов разработки.

Таже см. ниже про мониторинги API


### direct-features { #direct-features }

Инвайт-ссылка: <https://t.me/+3lYUunKoWBAwYjQy>  
Чат с уведомлениями об автоматическом обновлении фичей, после изменения в production.


### Direct.Features.Notifications { #direct-features-notifications }

Инвайт-ссылка: <https://t.me/+oNuW7YIeF1kwODcy>
Чат с еженедельными уведомлениями об увеличении количества просроченных фичей у владельцев


## Директ / автоматические мониториннги

### Direct.Monitoring.Calls { #Direct-Monitoring-Calls }

Инвайт-ссылка: <https://t.me/joinchat/BV5nDE20aOdKuG4yqTYKlg>

В этот чат дублируются звонящие проверки аппдьюти.  
Подписываются аппдьюти и все желающие.  
Человеческие разговоры в этом чате вести не надо, только отбивки "смотрю"/"занимаюсь".


### Direct.AppDuty.Monitoring {#Direct-AppDuty-Monitoring}

Инвайт-ссылка: <https://t.me/joinchat/BV5nDFZESvl3Sfu5lsIhLg>

Мониторинги Direct health.  
Подписываются аппдьюти и все желающие.  
Человеческие разговоры в этом чате вести не надо.


### Direct.Monitoring { #direct-monitoring }

Инвайт-ссылка: <https://t.me/joinchat/RIEnbjjZR2mF6uML>

Проверки, менее срочные, чем в Direct.AppDuty.Monitoring.  
Подписываются аппдьюти и все желающие.


### Мониторинги API { #direct-api-monitoring }

Есть чаты с мониторингами API:
- API Monitoring: общий мониторинг API, содержит много шумящих проверок.
- Group API Clean Monitoring: дополнение к API Monitoring, содержит только нешумящие проверки, которые потенциально можно передать app-duty.

Если нужно приглашение в эти чаты, обращайтесь в группу разработки API.



### Мониторинг группы разработки внутренних систем Директа { #DISMonitoring }
Закрытый чат для алертов (по большей части — production), не сданных в app-duty в силу разных причин.

Ответственный — [ppalex](https://staff.yandex-team.ru/ppalex).

### Мониторинг ошибок интерфейса
https://t.me/joinchat/zmPfHWlMGsYwMzBi

Ответственный - [alkaline](https://staff.yandex-team.ru/alkaline).

## Аналитика Директа

### [Директ] Аналитика { #direct-analytics }

Инвайт-ссылка: <https://t.me/joinchat/T4nNzD8gOYkEBcCD>

Чат с командой аналитики Директа. Здесь можно обсудить свою задачу, узнать, как её запланировать, или получить консультацию по работе с данными Директа.

## Соседние сервисы { #nearby-services }

### Модерация Директа { #directmod }

Инвайт-ссылка: <https://t.me/joinchat/AAAAAEHOKMZ_MUAHks42MQ>


### Баланс: аварии { #balance-incidents }

Инвайт-ссылка: <https://t.me/joinchat/Pkmm8GcE3zCgjypk>  
Уведомления об инцидентах Баланса

Но если в ошибках со стороны Баланса присутствует trust-payments \ balance-payments - первым делом лучше сходить в [Факапочную Траста](#trust-incidents)

### Баланс: вежливый чат (продакшен) { #balanse-prod }

Инвайт-ссылка: <https://t.me/+EsEI8M_PMlxmMDky>  
Разработка Баланса (продакшен). Prod-проблемы лучше сначала нести на рассылку balance-support@yandex-team.ru.

### balance-test-errors { #balance-test }

Инвайт-ссылка: <https://t.me/joinchat/AAAAAAt2OKDN9K2nvxuNjQ>  
Координация по проблемам тестового Баланса

### Факапочная Траста { #trust-incidents }
 
Инвайт-ссылка: <https://t.me/joinchat/IwXXtIRGsMUwMDU6>

### Траст обычный чат { #trust-common}

Инвайт-ссылка: <https://t.me/joinchat/9u0aFACyq4o0MTIy>
Общие вопросы про траст, проблемы с тестингом

### Поломки Рекламы (ex. БК-Директ-Метрика-Модерация всё ли хорошо?) { #adv-services }

Инвайт-ссылка: <{{chat-adv-incidents}}>  
Читать о проблемах в соседних сервисах рекламы;
писать о проблемах Директа, которые существенно затрагивают соседние рекламные сервисы;
репортить наблюдаемое неправильное поведение соседних рекламных сервисов.

Подробнее о чате: <https://wiki.yandex-team.ru/ads/nadezhnost-reklamnyx-texnologijj/ustranenie-polomok-aka-troubleshooting/>

### LSR рекламных технологий { #adv-lsr }
Инвайт-ссылка: <https://t.me/joinchat/BVB4ClL1Vs3gqnocYA2uwg>  
В чате анонсируются предстоящие к разбору инциденты.

### Канал со всеми SPI рекламы { #adv-spi }

Инвайт-ссылка: <https://t.me/joinchat/RmilNPaI10tDdmOr>  
Читать, принимать к сведению


### Метрика + Директ (Тестовые среды) { #metrika-test }

Инвайт-ссылка на чат в Мессенджере: <https://q.yandex-team.ru/#/join/3a76c929-12e0-4ef4-865c-d3debd3cbb20>


Чат в слаке: <https://yndx-ad-tech.slack.com/archives/C01F09BSR6Z>


Проблемы с тестовой метрикой


### ADVQ (и wordstat) { #advq }
<p style="text-decoration: line-through;" markdown="1">
Инвайт-ссылка: https://t.me/joinchat/BE-3JhHvWnTLA00nt_Xiag<br/>
Проблемы с ADVQ, влияющие на Директ (и наоборот).
</p>

[DEPRECATED] 2019-10: рекомендуют писать дежурным в чат [Статистика БК](#bs-stat) На самом деле какая-то активность происходит, писать в какой-нибудь общий чат типа [Статистика БК](#bs-stat) или [AppDuty](#direct-app-duty), чтобы добавили

### Контент-система БК { #cs-duty }

Сюда писать по всем вопросам, связанным с новым и старым транспортам в БК.
Инвайт-ссылка: <https://t.me/joinchat/FlT_0Q5bp-piY2Ni>

### Статистика БК { #bs-stat }

Инвайт-ссылка: <https://t.me/joinchat/Bq1XcEBwAgPjOrkc1xzsjw>

### Движок БК { #bs }

Инвайт-ссылка: <https://t.me/joinchat/AufO4z8tmC0PtnS0KDUSxw>  
Чат с дежурными БК. Проблемы с торгами

### CaeSaR Senate { #caesar }

Инвайт-ссылка: <https://t.me/joinchat/Vv2ThHO3EsE4MmU6> 

Чат с вопросами о системе цезарь <https://wiki.yandex-team.ru/bigb/caesar/>

### Справочник { #tycoon }
Инвайт-ссылка: <https://t.me/joinchat/BuMzDk_uMG_FuZpoQFEo4w>

### PCODE Support [Партнёрский код, ПКод, pcode] { #pcode }

Инвайт-ссылка: <https://t.me/joinchat/EHE5D0mx9ZnG2R5He-nunQ>

Дежурный в показывающем коде: <https://abc.yandex-team.ru/services/banners/duty/>

Дежурный по видеорекламе: <https://abc.yandex-team.ru/services/adsdk/duty/>

Релизы: <https://nda.ya.ru/t/y4XuATZ73fhfJp>

## Платформы / общие инфраструктурные сервисы { #global-infra }


### Solo { #solo }

Инвайт-ссылка: <https://t.me/joinchat/TvSc1SmLXfhk4fIu>

[Что такое solo](../glossary/glossary.md#solo).

### YT { #yt }

Инструкция, куда и как репортить проблемы в зависимости от критичности: <https://docs.yandex-team.ru/yt/problems/howtoreport>

Кроме того, есть `YT Seneca Lounge` &mdash; закрытый чат для срочных критичных проблем с динтаблицами у потребителей из рекламы.  
Инвайт-ссылки туда нет, если хочешь воспользоваться этим чатом &mdash; попроси в [админском чате](#direct-admin-chat), чтобы кто-нибудь тебя туда добавил.


### Zora (proxy) и Ротор (скриншотилка) { #zora-rotor }

Инвайт ссылка: <https://t.me/joinchat/CfwpTT8thXxCIp5TQi-CtQ>
Чат поддержки/консультации пользователей Zorа и Rotor

### Докцентр (doccenter, тултипы) { #doccenter }

Инвайт ссылка: <https://t.me/joinchat/DDUR5Er5mk8Vt5bJsHiSWQ>

### Logbroker { #logbroker }
Чат эксплуатации/разработки логброкера.  
Инвайт ссылка: <https://telegram.me/joinchat/BvmbJED8I3aGqqtk_ssAbg>,
[запасной чат в Q](https://q.yandex-team.ru/#/join/08a19f87-de45-4163-b37e-c1692e32455f), на случай проблем с телеграмом.

### MDB { #mdb }

Инвайт-ссылка: <https://t.me/joinchat/CCDG-0Dje_KWvyMQ-bFMtA> "mdb-support" ([источник](https://doc.yandex-team.ru/cloud/mdb/#kuda-obrashatsya-za-podderzhkoj))

### MDS { #mds }

Инвайт-ссылка: <https://t.me/joinchat/Lz2_8w1qRw7-PDRGLP3b3w> ([источник](https://wiki.yandex-team.ru/mds/#kontakty))  
Telegram Emergency chat — в случае срочных проблем затрагивающих живых пользователей в production

### Sandbox { #ya-sandbox }

Инвайт-ссылка: <https://t.me/joinchat/BLQp10XNMTrbGctZrctfGg>  
Чат Sandbox (https://sandbox.yandex-team.ru) про аварии.  
Не путайте Sandbox и [Песочницу API Директа](https://yandex.ru/dev/direct/doc/dg/concepts/sandbox-docpage/), которая по-английски тоже sandbox

### L3-балансеры { #l3-slb }

Инвайт-ссылка: <https://t.me/joinchat/BfOW3UJ_0OTgzpCoJ14huQ>  
Писать багрепорты, если балансеры делают странное


## Яндекс { #yandex }

### Координация больших факапов 2.0 { #global-incidents }

Инвайт-ссылка: <https://t.me/joinchat/BeUD0kQlNiNqon4C7SSIlQ>  
Координация больших факапов  
Читать и принимать к сведению

### Дежсмена (Марти) { #marti } { #marty }

Инвайт-ссылка: <https://t.me/joinchat/QBOqnOEY1vqhdmse>  
Сюда можно писать про проблемы с сервисами "под девятками", помогут найти правильных ответственных

### Регламентные работы { #dc-maintenance }

Инвайт-ссылка: <https://t.me/joinchat/PaZhvX5pm5phcPFN>  
Объявления о регламентных работах в ДЦ  
Читать и принимать к сведению

### Выручатик { #vyruchatik }

Инвайт-ссылка: <https://t.me/joinchat/Cb3k4EOO4qxVBNXOeZZjow>  
Координация на больших мероприятиях и при экстренных ситуациях
(пикнинки, корпоративы, эвакуации)

Инвайт-ссылка: <https://t.me/joinchat/A1c0Hkwa0Cl-2Nmvfcc39A>  
Филиал Выручатика в СПб

Инвайт-ссылка: <https://t.me/joinchat/UtT85vGZqPmVL_uH>  
Выручатик-Анархия — чат в котором можно флудить.


## Ссылки на другие списки { #other-lists }

<https://wiki.yandex-team.ru/devops/telegram/> — чаты для жалоб на gencfg, nanny, qloud etc.  
<https://wiki.yandex-team.ru/market/development/incident-routing/> — список Маркета  
<https://clubs.at.yandex-team.ru/sepe/2233> — резервные чаты в Ямбе

