[Дежурство "Релизы + ТС"](direct-releases-duty.md) <br/>
[Дежурство по 9999](9999-duty.md) <br/>

# App-duty в Директе

{% note warning "Переросло в Главный дежурный по продакшену" %}

Подробнее [тут](main-duty.md)

{% endnote %}

## Что это такое и зачем { #theory }

App-duty в Директе -- это начало реализации devops-концепции Яндекса.

Разработчики Директа присматривают за продакшеном и поддерживают его в хорошем состоянии.

График дежурств (дежурство full-time): <https://abc.yandex-team.ru/services/direct-app-duty/duty2/30725>


## Формат смен { #shifts }

Одновременно дежурят два человека.
Смены по неделе сб и вс включительно.


## Подбор дежурных { #recruitment }

- справедливое количество дежурных: половина штатных разработчиков Директа
- очередных кандидатов в дежурные выбираются руководителями

## Передача дежурства { #shift-change }

1. В понедельник и в четверг в 11:00 робот пишет напоминалку в админский чат "пора меняться", [кронтаб](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/ppcdev-scripts-cron/etc/cron.d/yandex-du-ppcdev-scripts-cron?rev=r7743382#L69)
1. Дежурные меняются, [инструкция](duty_start_shift.md), в частности:
   1. Сменяемые дежурные пишут в дежурном тикете и в чате, что надо иметь в виду новым дежурным
   1. Переключают звонки
1. В 11:00 предыдущие и новые дежурные вместе с pe4kin@ собираются на [встречу](https://calendar.yandex-team.ru/event/66009657) "передача дежурства"
   1. Если актуально, предыдущие дежурные рассказывают сложные обстоятельства от предыдущего дежурства
   1. Актуализируем дашборд <https://st.yandex-team.ru/dashboard/67567>

{% cut "потеряло актуальность/устарело/переехало в другие разделы" %}

## Адаптация новых дежурных { #adaptation }

1. Добавить новых дежурных в аппдьютевый чат
1. Включить новых дежурных в abc-сервис direct-app-duty, роль "Разработчик" <https://abc.yandex-team.ru/services/direct-app-duty/>
1. Включить новых дежурных в abc-сервис direct, роль "Участник app-duty" <https://abc.yandex-team.ru/services/direct/>
1. Добавить новых дежурных в два дежурства в duty.mtrs <https://duty.mtrs.yandex-team.ru/project/direct/> (app-duty-1, app-duty-2)
1. Включить новых дежурных в расписание, подробнее на [странице](../jeri/app-duty-schedule.md)
1. Добавить новых дежурных в регулярную встречу
1. Провести вводную встречу
1. Написать на каждого дежурного тикет "Новый app-duty", по образцу предыдущих, с тегом app_duty_newcomer, [фильтр](https://st.yandex-team.ru/issues/?_o=created+DESC&_f=type+priority+key+summary+description+status+resolution+created+updated+assignee+parent&tags=%22app_duty_newcomer%22)

## Дежурство { #tasks }

### Реагирование { #tasks-response }

1. Несколько раз в день в админском чате робот пишет, какие релизы ждут выкладки, подробнее см. [на странице](../concepts/releases/deploy-schedule)
1. Чат со звонящими мониторингами
1. Жалобы на Директ в Тревожном чате и чате БК-Директ-Метрика
1. Чат Direct.AppDuty.Monitoring
1. Вопросы в админском чате


### Другие задачи { #tasks-doing }

По плану, принятому на полуденной встрече в начале смены.
Все актуальные задачи -- на доске <https://st.yandex-team.ru/agile/board/13065>



## Регулярные действия { #recurrent-actions }

- составление расписания дежурств, см. [страницу](../jeri/app-duty-schedule.md)
- встречи app-duty, раз в 3 недели, <https://wiki.yandex-team.ru/jeri/app-duty/meetings/>
- ...
- [тикеты адаптации новых аппдьюти](https://st.yandex-team.ru/issues/?_o=created+DESC&_f=type+priority+key+summary+description+status+resolution+created+updated+assignee+parent&tags=%22app_duty_newcomer%22)


## TODO { #todo }

Что хорошо добавить на эту страницу:

- про области, к которым прикладывают усилия дежурные
- больше ссылок про чаты и мониторинг
- про образовательные усилия (возможно, отдельную страницу и ссылку)
- ...

{% endcut %}

## Ссылки { #links }


- основной abc-сервис <https://abc.yandex-team.ru/services/direct/>
- abc-сервис дежурных <https://abc.yandex-team.ru/services/direct-app-duty/>
- [составление расписания](../jeri/backend-duty-schedule.md)
- инструкция по переключению дежурств <https://wiki.yandex-team.ru/jeri/app-duty/duty-change/>
- agile-борда <https://st.yandex-team.ru/agile/board/13065>
- вопросы ко встречам <https://wiki.yandex-team.ru/jeri/app-duty/meetings/>

