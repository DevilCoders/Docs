# Регулярный отчёт с аккаунтами МТС.Музыки

Делали в тикете — [PASSP-32777](https://st.yandex-team.ru/PASSP-32777)

YQL-cкрипт [mts_music_uids.yql](mts_music_uids.yql) находится в https://yql.yandex-team.ru/Queries/60b4acfabf78864989d693b3

YRE-скрипт [mts_music_uids.yre](mts_music_uids.yre) находится в реакции [/passport/production/Создать отчёт с аккаунтами МТС.Музыки](https://reactor.yandex-team.ru/browse?selected=9006447)


## Алгоритм составления отчёта

* Социализм ежедневно [создаёт](https://a.yandex-team.ru/arc/trunk/arcadia/passport/python/social/dumpers/upload_profile_crypta.py?rev=r8229569#L210) таблицы с соц. профилями в YT — [hahn.//home/passport/production/socialism/crypta-dump](https://yt.yandex-team.ru/hahn/navigation?path=//home/passport/production/socialism/crypta-dump)
* Для каждой таблицы публикуется новая версия артефакта в Реакторе - [/passport/production/hahn/home/passport/production/socialism/crypta-dump](https://reactor.yandex-team.ru/browse?selected=9019523)
* На публикацию версий артефакта настроена реакция - [/passport/production/Создать отчёт с аккаунтами МТС.Музыки](https://reactor.yandex-team.ru/browse?selected=9006447)
* Эта реакция, используя YRE и YQL скрипты, создаёт из таблицы с соц. профилями таблицу с аккаунтами МТС.Музыки в YT - [hahn.//home/passport/production/socialism/mts/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/passport/production/socialism/mts/latest)


## Используемые роботы

[Робот Социализма](https://staff.yandex-team.ru/robot-ironfelix) создаёт таблицы с соц. профилями и публикует новые версия соответсвующего артефакта

[Робот robot-pssp-analytics](https://staff.yandex-team.ru/robot-pssp-analytics) запускает YQL-скрипт, читает таблицу с соц. профилями и создаёт таблицу с аккаутами МТС.Музыки
