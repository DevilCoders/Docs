# Входная точка для новых пользователей
## Доступы

{% note tip %}

Окнуть доступы в панчере вам смогут в чате: [taxi-ito-helpline]({{ ito_helpline_chat_link }}).

{% endnote %}


### Тулза генерации правил
При использовании [генератора правил]({{ link_to_gen_rules }}) нужны дырки в тестинг репликации из виртуалки до
`replication.taxi.tst.yandex.net`, запрашивать через панчер.
Возможно, доступы у вас уже будут. Если их нет, воспользуйтесь ссылкой на
[форму в панчере](https://puncher.yandex-team.ru/?create_comment=%D0%94%D0%BB%D1%8F%20%D0%B3%D0%B5%D0%BD%D0%B5%D1%80%D0%B0%D1%86%D0%B8%D0%B8%20%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%20%D1%80%D0%B5%D0%BF%D0%BB%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D0%B8&create_destinations=replication.taxi.tst.yandex.net&create_locations=office,vpn&create_ports=80&create_protocol=tcp&create_until=persistent)

- Пример запроса с виртуалки: [http://st.yandex-team.ru/DOSTUPREQ-234237](http://st.yandex-team.ru/DOSTUPREQ-234237)
- Если запускаете локально: [http://st.yandex-team.ru/DOSTUPREQ-233618](http://st.yandex-team.ru/DOSTUPREQ-233618)

### Доступ к админке
Если админка {{ description_replication_admin }} вообще не открывается, нужно получить дырки в панчере, примеры:
- **testing**: [https://st.yandex-team.ru/DOSTUPREQ-234384](https://st.yandex-team.ru/DOSTUPREQ-234384)
- **production**: [https://st.yandex-team.ru/DOSTUPREQ-234385](https://st.yandex-team.ru/DOSTUPREQ-234385)

Далее, если админка открывается, но разделы все еще недоступны, нужны следующие доступы:
- **testing**: [IDM: superuser](https://idm.yandex-team.ru/system/taxiadmintest/roles#rf=1,rf-role=nqBwNnrL#taxiadmintest/superuser(fields:()),f-status=all,f-role=taxiadmintest,sort-by=-updated,rf-expanded=nqBwNnrL)
- **production**: [IDM: Просмотр правил, создание драфтов, просмотр логов](https://idm.yandex-team.ru/system/taxiadmintest/roles#rf=1,rf-role=nqBwNnrL#taxiadmin/group-6d749ed17c804193bf9b761e2700967f(fields:()),rf-role=uVq7ASXU#taxiadmin/group-54fac98013b9465b88837c2d851f1147(fields:()),rf-role=bI5tSpAG#taxiadmin/group-a35b34bfa8504a3ca279330951611c0b(fields:()),rf-role=XH1lgmC4#taxiadmin/group-config_ro(fields:()),rf-role=TDkTTcj2#taxiadmin/group-24bc96cb7b9e4c6abb93d259ad4da9ba(fields:()),f-status=all,f-role=taxiadmintest,sort-by=-updated)

За оком обращатейсь к указанным в IDM-заявке людям.
На аппрувы драфтов (изменений) в проде есть отдельная [инструкция](responsible.md), но этим оптимальнее заняться позже, после создания первого правила

### Просмотр логов в кибане
На предыдущем шаге логи можно было посмотреть и в админке кронов. Иногда этого не хватает, стоит получить дырки до кибаны.
- [Пример запроса в панчере](https://st.yandex-team.ru/DOSTUPREQ-235678)

### Доступы к тимсити для релизов и тестинга
Доступы к `teamcity.taxi.yandex-team.ru` уже должны [быть](https://puncher.yandex-team.ru/?id=61f2a4459ceb3013406e5921) у всех.

### Доступ к источникам {#connections}
Когда вы готовы создавать правило, стоит получить доступы к источнику и добавить секреты: [подробнее](secrets.md#puncher).

### Доступ к тарегтам {#targets}
[Инструкция для YT](yt_prefixes.md).
