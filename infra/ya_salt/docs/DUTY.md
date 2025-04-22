## Инструкция для дежурного
Попробуем собрать здесь набор инструкций, помогающих и направляющих дежурных по компоненту hostmanager.

### Обязанности дежурного
  * Выкладка PR'ов в salt.
  * Реакция на призывы во внутренние чаты по проблемам.
  * Реагирование на алерты мониторинга в чате [[RTC] Monitoing](https://t.me/joinchat/CBL7wFJ8ZMRdZk5ApGCgIw), общую картину можно увидеть на [корневых аггрегатах](https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3DRTC%26tag%3Dlevel_root&limit=160&view=tiles)
  * Активный polling чата [[RTC] Внутренний](https://t.me/joinchat/BtjT40RP8gP5ishgHuoRKQ) на предмет дискуссий по проблемам, где мы можем быть полезны.
  * Дополняет данный регламент, улучшает средства мониторинга
  * Разбирает SPI тикеты - занимается инцидент менеджментом.
  * Разбирает тикеты с тэгом [#duty в очереди HOSTMAN](https://st.yandex-team.ru/HOSTMAN/order:assignee:false/filter?resolution=empty()&tags=duty)
  * В помощь в разборе тикетов для дежурного есть [дашборд](https://st.yandex-team.ru/dashboard/31315). Если на нем чего-то не хватает - feel free to improve it.
  * Обновление gencfg тега (раз в неделю, [выбираем](https://gencfg.yandex-team.ru/status) и [прописываем](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/browse/search_runtime/_pillars/gencfg-version.sls))

## Выкладка
Выкладка - итерация, merge commit'ов в локационные ветки. Последовательность действий дежурного выглядит так:
  * Просмотр PR'ов в develop.
  * Merge их в develop.
  * Последовательный merge веток:
    * develop -> master_sas
    * master_sas -> master_vla
    * master_vla -> master_man
    * master_man -> master_msk

### Работа с PR'ами.
Отсматриваем [PR'ы в develop](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/pull-requests).
Каждый PR должен быть:
  * В ветку `develop`.
  * Тесты должны быть пройдены.
Дежурный должен визуально отсмотреть изменения на предмет логических и синтаксических ошибок.

Перед началом каждой итерации дежурный __на своё усмотрение__ выбирает набор PR'ов, которые "поедут" в этой итерации.
Каких-то формальных критериев выбора нет, следует ориентироваться на то, чтобы изменений не было слишком много.

У каждого выбранного PR'а нажимаем кнопку `Merge` и смотрим на панель [HOSTMANAGER ctype=prestable](https://yasm.yandex-team.ru/template/panel/HOSTMANAGER/ctype=prestable/)
на предмет ошибок.

### Время работы
Выкладки солта проходят каждый день (с понедельника по пятницу) с 11:00 до 19:00 по Мск.

### Перед стартом
Необходимо убедиться, что на рабочей станции дежурного собран CLI orly: `ya make infra/orly/ctl`,
чтобы быть готовым остановить выкладки в случае проблем.

### Итерация
После того, как выкладка в prestable произошла (она может показать уверенно только синтаксические ошибки), нужно начинать выкладку по ДЦ.
Начинаем:
  * Создаём PR [develop -> master_sas](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/pull-requests?create&targetBranch=refs%2Fheads%2Fmaster_sas&sourceBranch=refs%2Fheads%2Fdevelop&targetRepoId=4683&title=DEV%20%3D%3E%20SAS)
  * Просим коллег подтвердить.
  * Нажимаем `Merge`.
  * Открываем:
    * панель [HOSTMANAGER geo=sas](https://yasm.yandex-team.ru/template/panel/HOSTMANAGER/geo=sas/)
  * Ждём, когда количество `CHANGED states` вернётся на первоначальный уровень.

Далее повторяем действия по ДЦ:
  * PR [master_sas -> master_vla](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/pull-requests?create&targetBranch=refs%2Fheads%2Fmaster_vla&sourceBranch=refs%2Fheads%2Fmaster_sas&targetRepoId=4683&title=SAS%20%3D%3E%20VLA)
    * панель [HOSTMANAGER geo=vla](https://yasm.yandex-team.ru/template/panel/HOSTMANAGER/geo=vla/)
  * PR [master_vla -> master_man](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/pull-requests?create&targetBranch=refs%2Fheads%2Fmaster_man&sourceBranch=refs%2Fheads%2Fmaster_vla&targetRepoId=4683&title=VLA%20%3D%3E%20MAN)
    * панель [HOSTMANAGER geo=man](https://yasm.yandex-team.ru/template/panel/HOSTMANAGER/geo=man/)
  * PR [master_man -> master_msk](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/pull-requests?create&targetBranch=refs%2Fheads%2Fmaster_msk&sourceBranch=refs%2Fheads%2Fmaster_man&targetRepoId=4683&title=MAN%20%3D%3E%20MSK)
    * панель [HOSTMANAGER geo=msk](https://yasm.yandex-team.ru/template/panel/HOSTMANAGER/geo=msk/)

### В случаем проблем
* Остановить выкладку через Orly
  > для выставить Orly правило в 0
  > для prestable - [salt-state-apply-prestable](https://a.yandex-team.ru/arc/trunk/arcadia/infra/orly/rules/salt-state-apply-prestable.yaml)
  > для production - [salt-state-apply](https://a.yandex-team.ru/arc/trunk/arcadia/infra/orly/rules/salt-state-apply.yaml)
* Откатить релиз
  > в bb на странице проблемного PR нажать кнопку revert (спрятана в меню сверху)
  > создастся PR откатывающий изменения
  > ![Revert](https://a.yandex-team.ru/arc/trunk/arcadia/infra/ya_salt/docs/revert-button.jpg)
