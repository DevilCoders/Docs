# Инструкции к проверкам
## [portal.morda.web:backend.ab_flags_test_touch](https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Dbackend.ab_flags_test_touch){#portal.morda.web:backend.ab_flags_test_touch}
#### Что значит его срабатывание
Сломались эксперименты
#### Какой ущерб наносится пользователю и компании
Большой. Эксперименты вероятно не работают.
#### Что делать
Сразу идти к Марти и сказать, что вероятно сломались эксперименты.
Дока от ivan-karev@ [https://wiki.yandex-team.ru/morda/duty/experiments/](https://wiki.yandex-team.ru/morda/duty/experiments/)
Чат экспериментов: [https://t.me/joinchat/CyCSrknStrKg0dT24S2GXA](https://t.me/joinchat/CyCSrknStrKg0dT24S2GXA)

---
## [portal.morda.web:backend.ab_flags_test_desktop](https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Dbackend.ab_flags_test_desktop)
Аналогично [backend.ab_flags_test_touch](#portal.morda.web:backend.ab_flags_test_touch)

---

## [portal.morda.app:backend.errors.nodata.ski](https://juggler.yandex-team.ru/check_details/?host=portal.morda.app&service=backend.errors.nodata.ski)
#### Что значит его срабатывание
Отсутвуют какие либо данные для горнолыжки на морде. Данные получаем [отсюда](https://s3.mds.yandex.net/rtx-public/ski/ski-resorts.json). Горнолыжка делалась [тут](https://st.yandex-team.ru/HOME-74802)
#### Какой ущерб наносится пользователю и компании
Могут не показываться горнолыжные шорткат, фулскрин, алерт.
#### Что делать
Локализовать проблему и отнести [@danildudin](https://staff.yandex-team.ru/danildudin), [@alexeybabenko](https://staff.yandex-team.ru/alexeybabenko), [@baibik](https://staff.yandex-team.ru/baibik).

## [portal.morda.app:backend.request_yabs_options_count_touch](https://juggler.yandex-team.ru/check_details/?host=portal.morda.app&service=backend.request_yabs_options_count_touch)
#### Что значит его срабатывание
Превышен лимит на количество запрашиваемых у ябса bk-флагов, в следствие чего, часть флагов приходить не будет. Текущий лимит - 75.
#### Какой ущерб наносится пользователю и компании
Могут не показываться некоторые алерты, блоки, шорткаты - все то, что откручивается по bk-флагам.
#### Что делать
Сходить к менеджерам и попросить вычистить лишнее из экспорта [yabs_flags](https://madm.yandex-team.ru/edit?export_file=yabs_flags&stage=production)

## [portal.morda.web:big_type_low](https://juggler.yandex-team.ru/check_details/?host=portal.morda.web&service=big_type_low)
#### Что значит его срабатывание
Просадка траффика в десктопную морду.
Алерт показывает долю big от touch+mob.
#### Какой ущерб наносится пользователю и компании
Для пользователя возможно показ CAPTCHA вместо морды. Для компании возможно потеря доли.
#### Что делать
1. Посмотреть на график срабатываний антиробота на панели дежсмены: https://yasm.yandex-team.ru/template/panel/morda_lights_dezh/mode=full. Если это оно, то светофор из-за приходивших ботов недавно, он трендовый и скоро погаснет
2. Если причина срабатывания по-прежнему остаётся непонятной, обратиться за помощью к SRE. Если на графике алерта (именно на графике, так как алерт трендовый и будет продолжать гореть даже после нормализации) все вернулось в норму, то расследовать можно в рабочее время, смотреть по ситуации.

## [portal.morda.app.android_search_app_morda_card_error_summ](https://juggler.yandex-team.ru/check_details/?host=portal.morda.app&service=android_search_app_morda_card_error_summ)
#### Что значит его срабатывание
Увеличение клиентских ошибок в ПП. Новая версия ПП раскатывается плавно. Алерт может сработать с опозданием.
#### Какой ущерб наносится пользователю и компании
Ф-ность на клиенте может не работать. Может быть заметно пользователю.
#### Что делать
1. Ошибки можно посомотреть в [ErrorBooster](https://nda.ya.ru/t/qy2hAxu03qV2GF)
Есть [yasm panel](https://nda.ya.ru/t/9vtICOAq3W2ggS) (TODO: описать эту панельку)
2. Написать в чат [Факапочная мобильной морды](https://t.me/joinchat/BEdJXBlXz0dBmZGck_IiDQ)
3. Дежурный клиенской разработки может признать ошибки нормой или временной нормой:
    * Увеличить порог алерта [в этом шаблоне](https://yasm.yandex-team.ru/template/alert/portal.morda.app/)
    * Создать тикет вернуть порог обратно, если требуется
4. Морда (бэк или фронт) могут что-то не присылать, присылать лишнее
    * Найти и призвать к обсуждению автора изменений
    * Связать ошибки с релизом; с каким-то включение фичи

## [portal.morda.tests.perl_tests_is_alive](https://juggler.yandex-team.ru/check_details/?host=portal.morda.tests&service=perl_tests_is_alive)
#### Что значит его срабатывание
Перловые тесты **perl tests** в пуллреквестах не запускались больше полутора суток. Норма, если проверка сработала в праздничные дни, когда никто не коммитит.
#### Какой ущерб наносится пользователю и компании
Пользователи не страдают. Разработчики могут не заметить, что что-то сломалось правками кода.
#### Что делать
Сходить к @core.

## [portal.morda.frontend:home.4xx](https://juggler.yandex-team.ru/check_details/?host=portal.morda.frontend&service=home.4xx&last=1DAY)
#### Что значит его срабатывание
Проблемы с загрузкой статики в бакете home. В error booster'e https://s3-int.chv.yandex-team.ru/projects/home/projectDashboard определяем какой из 4xx статусов фонит:
  * `404`. В telegram чате morda backend команда /static, выбираем нужный бакет, форвардим top в чат покатушек с призывом дежурных менеджеров. Если проблема не локализуется, тогда отнести в L7-balancer-support https://t.me/joinchat/Cbhulkz_7ZPg6vJdCrcMpg. Более подробное описание как дебажить с примерами YQL запросов лежит тут https://wiki.yandex-team.ru/morda/sre/#monitoringstatikinamorde
  * `429`. Запросы блокируются на стороне mds. Обратиться в telegram чат MDS/Avatars/S3/Yarl support https://t.me/joinchat/Bbsak0DREDckUOGhK-m3aw с просьбой о помощи с указанием проблемного бакета.

## [portal.l7_term.pumpkin](https://juggler.yandex-team.ru/check_details/?host=portal.l7_term&service=pumpkin&last=1DAY)
#### Что значит его срабатывание
Инфраструктура не смогла обработать запрос и пользователь увидел старую железную тыкву (выглядит как ya.ru)
#### Какой ущерб наносится пользователю и компании
Большой. Хуже тыквы только показ пустой страницы.
#### Что делать
Локализовать до конкретного сигнала (алерт внутри содержит сумму сигналов) - например, ```balancer_report-report-morda_requests_to_knoss_onerror-requests_summ```
Собрать диагностику в [YQL запросом](https://yql.yandex-team.ru/Operations/YPaivfMBw55cXr0NzcBRqSICtqY4La1VRhLXjH2GAkw=) типа:
```
USE Hahn;
SELECT
    *
FROM hahn.`logs/l7-balancer-access-log/stream/5min/2021-07-08T13:55:00`
where workflow like '%morda_requests_to_knoss_onerror%'
LIMIT 100;
```
Выбрать нужный отрезок логов (если они уже доехали) и вставить правильное значение в конструкцию like.
После выполнения запроса изучить содержимое поля workflow, где написана причина. Дальше действовать по ситуации.

## [portal.morda.apphost:apphost.failures.all](https://juggler.yandex-team.ru/check_details?host=portal.morda.apphost&service=apphost.failures.all)
#### Что значит его срабатывание
#### Какой ущерб наносится пользователю и компании
#### Что делать
Пойти в [еррор-бустер](https://error.yandex-team.ru/projects/apphost/errors/2640476060625735591/errorDashboard?componentSettings=%7B%22row_1_col_0_con_0_charts%22%3A%7B%22scale%22%3A%22hour%22%7D%7D&filter=service%20%3D%3D%20MORDA) → посмотреть на ошибки → посмотреть в <b>Request IDs</b> → выбрать там <b>setrace</b> → понять где обламался запрос


## [portal.morda.function_tests:schema.api_search_rf_works.failed](https://juggler.yandex-team.ru/check_details/?host=portal.morda.function_tests&service=schema.api_search_rf_works.failed&last=1DAY)
#### Что значит его срабатывание
Возможно что-то случилось с откруткой бк флагов в андроид ПП
#### Какой ущерб наносится пользователю и компании
Может увеличиться задолб промотированием и алертами
#### Что делать
Сходить [сюда](https://solomon.yandex-team.ru/?project=yabs&cluster=frontend_partner&server_group=_ALL_&service=frontend_meta_ext_requests&host=Sas&dashboard=yabs_frontend_ext_request_detailed&l.handler=meta&l.ext_service=bigb_user_storage&b=7d21h&e=), посмотреть на графики.

Когда в прошлый раз отвалилась открутка, графики выглядели [вот так](https://jing.yandex-team.ru/files/alexeybabenko/Screenshot%20from%202021-09-23%2011-32-21.png ).

Если с графиками все плохо, написать в БК, можно попробовать [Никите Игнатову](https://staff.yandex-team.ru/naignatov) или другим участникам [SPI](https://st.yandex-team.ru/SPI-26575)

Если с графиками все нормально, то можно проверить [джобы MORDA_TEST_RF в сэндбоксе](https://sandbox.yandex-team.ru/schedulers?author=alexeybabenko&limit=20&created=14_days), все ли с ними нормально, глянуть логи, спросить @alexeybabenko.

Более подробно пожно прочитать в [таске про эту проверку](https://st.yandex-team.ru/HOME-72202).

## [portal.ddos_detector:infra.volume_root.usage_percent.vla](https://juggler.yandex-team.ru/check_details/?host=portal.ddos_detector&service=infra.volume_root.usage_percent.vla)

#### Что значит его срабатывание
Потребление дискового пространства превысило порог в 85%
#### Какой ущерб наносится пользователю и компании
Если вовремя не среагировать возможна частичная работоспособность пода и влияние на выдачу
#### Что делать
Зайти на под и почистить логи.

## [portal.apphost.morda.web.zen_ssr_requests.sas|man|vla](https://juggler.yandex-team.ru/check_details/?service=zen_ssr_requests.sas&host=portal.apphost.morda.web&last=1DAY)

#### Что значит его срабатывание
Наливаем лишний трафик в локацию Дзена, который может не выдержать. По договорённости отсюда https://st.yandex-team.ru/HOME-74799
#### Какой ущерб наносится пользователю и компании
Дзен может сломаться
#### Что делать
Если это результат учений, тогда остановить прогрузку и пересчитать таргет прогрузки, чтобы не было превышения. Таргет меняется [здесь](https://uchenki.yandex-team.ru/settings/service/morda).

## [portal.l7_knoss:porto_cpu_wait](https://juggler.yandex-team.ru/check_details/?host=portal.l7_knoss&service=porto_cpu_wait)

#### Что значит его срабатывание
Не хватает ресурсов CPU. Причины могут быть разные - от глюка балансера до проблем с железом
#### Какой ущерб наносится пользователю и компании
Тормозим, потом таймаутим
#### Что делать
Сообщить в чат [Balancer Releases [bin+cfg]](https://t.me/joinchat/UWhylyxFwrSvlBlJ).

## [portal.morda.sources:personal_request_batch_0.fails.morda](https://juggler.yandex-team.ru/project/portal/aggregate?host=portal.morda.sources&service=personal_request_batch_0.fails.morda)

#### Что значит его срабатывание
Сломались батчевые запросы в датасинк. Запросы могут быть с индексом от 0 до N.
Обычно personal_request_batch_0 - это получение настроек пользователя, а personal_request_batch_1 - сохранение настроек пользователя. Запросы с другими индексами могут быть как на изменение, так и на получение настроек пользователя.
https://wiki.yandex-team.ru/disk/datasync/about/

#### Какой ущерб наносится пользователю и компании
Не подгружаются настройки пользователя(счетчик непрочитанных писем, настройка темной темы, нотификации, карты лояльности...).

#### Что делать
[Идем в ErrorBooster](https://morda-plain-error.chv.yandex-team.ru/message?filter=type%20%3D%3D%20subreqfail%20AND%20subtype%20%3D%3D%20personal_request_batch%3A0) и находим текст ошибки.
Сообщить в чат - [Чат поддержки DataSync](https://t.me/joinchat/Dd--B0fE9-g9XFl7BVMnLQ), что батчевые запросы от морды падают с ошибкой(текс ошибки из ErrorBooster). В личку тоже можно писать, из админов у нас ignition@ главный
[ABC](https://abc.yandex-team.ru/services/DSAPI)

## [portal.morda.sources:personal_request_single_0.fails.morda](https://juggler.yandex-team.ru/project/portal/aggregate?host=portal.morda.sources&service=personal_request_single_0.fails.morda)

#### Что значит его срабатывание
Сломались одиночние запросы в датасинк. Запросы могут быть с индексом от 0 до N.
Раньше это были батчевые запросы с одним подзапросом. Для таких запросов стали делать одиночный запрос в датасинк, вместо батчевого, что экономит по оценке датасинка 10% cpu

#### Какой ущерб наносится пользователю и компании
Не подгружаются настройки пользователя.

#### Что делать
Тоже что и при поломке portal.morda.sources:personal_request_batch_0.fails.morda

## [portal.morda.sources:station_greetings.fails.morda](https://juggler.yandex-team.ru/check_details/?host=portal.morda.sources&service=station_greetings.fails.morda)

#### Что значит его срабатывание
На запросы станции или модуля в ответ получена ошибка
#### Какой ущерб наносится пользователю и компании
Юзер не может пользоваться железом (вероятно)
#### Что делать
Сообщить в чат [Alice Duty].
 
## [portal.morda.web:ab_flags_empty_export](https://juggler.yandex-team.ru/check_details/?host=portal.morda.web&service=ab_flags_empty_export&last=1DAY)

#### Что значит его срабатывание
При использовании модуля `MordaX::Experiment::AB` почему-то не удалось загрузить ab-флаги из экспорта `ab_flags_v2`. Одной из причин может быть слишком раннее использование модуля, когда не полностью завершилась инициализация morda_content, geo, device и пр. Также могли отломаться флаги из заголовков, их стоит проверить.
#### Какой ущерб наносится пользователю и компании
Не работает часть, возможно существенная, экспериментов.
#### Что делать
Смотреть, что катили или включали с использованием `MordaX::Experiment::AB` и срочно откатывать, отключать или действовать по ситуации.
Посмотреть на панели:
- отпашенные testid из заголовков - https://yasm.yandex-team.ru/panel/morda_ab_flags_lights
- флаги из экспорта - https://yasm.yandex-team.ru/panel/ab_flags_export

## [portal.greenbox:topnews_data_age](https://juggler.yandex-team.ru/project/portal/aggregate?host=portal.greenbox&service=topnews_data_age&project=portal)
## [portal.greenbox:topnews_new_data_age](https://juggler.yandex-team.ru/project/portal/aggregate?host=portal.greenbox&service=topnews_new_data_age&project=portal)

#### Что значит срабатывание
Возраст экспорта новостей в гринбоксе. Основные причины срабатывания:
 - экспорт пуллер не справляется с своевременной доставкой данных
 - данные не могут дойти до редиса, возможно сломался мастер редиса

#### Какой ущерб наносится пользователю и компании
На момент написания документации в гринбоксе живут только новости. Если ломаются рантайм новости и обновление данных в гринбоксе, значит новости на стороне пользователя перестанут обновляться.

#### Что делать
[Инструкция по диагностике мастера редиса](https://docs.yandex-team.ru/portal/projects/greenbox/master_switch)


## [portal.morda.exports:import.tv_schedule_kubr](https://juggler.yandex-team.ru/check_details/?host=portal.morda.exports&service=import.tv_schedule_kubr)

#### Что значит срабатывание
Поломка загрузки/парсинга телепрограммы, подробнее смотрим в лог соответствующего скрипта

#### Какой ущерб наносится пользователю и компании
Потенциально - большой, если не будет актуальной программы телепередач

#### Что делать
[Инструкция по импорту данных](https://wiki.yandex-team.ru/instrukcijapoimportam/)

