# Регламент дежурств по релизам

[График дежурств](https://abc.yandex-team.ru/services/direct/duty/?role=2228) по релизам  
Релизный [dashboard](https://st.yandex-team.ru/dashboard/50158)  
Релизный чат [direct-release]({{chat-direct-release}}), [чат дежурных]({{chat-release-duty}})

**Дежурный тестировщик отвечает за релизы dna, web, perl.**

Инструкции по тестированию: [dna](../../guide/releases/dna.md),
[web](../../guide/releases/java-web.md),
[perl](../../guide/releases/perl.md)

### Перед дежурством
**Дежурный тестировщик:**
1. Раскладывает ключи [по инструкции](../../guide/initial-setup/gpg-key.md) и настраивает [окружение](../../guide/releases/before-first-java-release.md)
2. Вступает в [чат]({{chat-release-duty}}) для дежурных по релизу
3. Идет на [встречу по передаче дежурств](https://calendar.yandex-team.ru/event/?event_id=57336675&uid=1120000000014295) в пятницу перед началом своего дежурства и получает всю необходимую информацию по статусам релизов от предыдущих дежурных
4. Ежедневно в 13:00 синкается по статусу релизов [на общей встрече по дежурствам](https://calendar.yandex-team.ru/event/57375429)
5. Всеми силами старается выкатить протестированный релиз в окно 14:00! :)

### Сборка релиза
1. Релиз начинает собираться по крону каждый день в 7:30 или сразу после выкладки предыдущего релиза. Кроме релизов perl - они не собираются автоматически (пункт 5).
2. После завершения автосборки в релизный чатик приходит сообщение от бота о результатах: успешно или неудачно завершилась сборка.
3. Если сборка завершилась успешно, то переходим к тестированию релиза.
4. Если сборка завершилась неудачно, то нужно оперативно начать решать проблему:
   - локализовать проблему и быстро пофиксить  
или  
   - призвать дежурного разработчика или более опытного коллегу (если дежурный затрудняется) для ускорения починки сборки
5. Оценить нужна ли сборка релиза perl: в транке 5 и более коммитов, есть зависимости от релиза perl, есть просьба собрать релиз perl от коллег. Для сборки релиза perl нужно выполнить команду `direct-release -s testing -a direct create-release`. Если сборка упала `direct-release -a direct -s testing continue-create-release`

### Тестирование релиза
**Дежурный тестировщик:**
1. Отслеживает релизы по [борде](https://st.yandex-team.ru/dashboard/50158)
2. Запускает регрессию на асессоров сразу после окончания сборки релиза [по инструкции](https://docs.yandex-team.ru/direct-dev/reference/assessors/regression-assessors)
3. Тестирует свои задачи в релизе и следит, чтобы задачи других QA не подвисали - в чатик приходят отбивки от бота о непротестированных тикетах в релизе с призывом QA задач - пингует их при необходимости и перевешивает задачи на других QA для ускорения тестирования релиза.
4. Анализирует результаты выполнения регрессии асессоров, заводит баги на разработку: 
   - если найден баг на ТС, то заводит на дежурного разработчика и линкует к релизному тикету, принимает решение о критичности багов к релизу совместно с менеджерами и дежурными
   - если найден баг прода, то заводит его отдельно
   - если найден баг в кейсе или проблема в тестовых данных, то фиксит yml к моменту следующего запуска регрессии на асессоров (до сборки следующего релиза!).
5. Следит за разбором дежурным разработчиком результатов выполнения автотестов, помогает и пушит фикс багов и самих автотестов при необходимости.

**QA задач, вошедших в релиз:**
1. Делает смоук по своим задачам, попавшим в релиз, в приоритетном порядке (приоритетнее могут быть только хотфиксы в прод)
2. По окончании тестирования задач в поле `Tested apps` выставляет приложение в релизе которого был протестирован тикет
3. При обнаружении бага в релизе заводит баг и линкует его к релизному тикету, оставляет в релизном тикете комментарий вида _"Найден баг в релизе DIRECT-XXX"_

### Проблема на тестовой среде, не связанная с кодом релиза
**Дежурный тестировщик:**
1. Завести тикет по [шаблону](https://st.yandex-team.ru/createTicket?template=7336&queue=DIRECT), сообщить о проблеме в [чат]({{chat-release-duty}}). При необходимости пушить и координировать проблему. 
2. Следит за чатом dev-talks если туда написали о прооблеме с тестовой средой то делает шаги из предыдущего пункта. 

### Хотфиксы в релиз
**Менеджер задачи, требующей хотфикса:**
1. Пишет обоснование необходимости хотфикса своей задачи в актуальные релизные тикеты [по шаблону](https://st.yandex-team.ru/settings/templates/comments?name=hotfix%20approve%20comment&owner=1120000000014295&queue=DIRECT) всех затронутых приложений. Найти релизный тикет можно на [борде](https://st.yandex-team.ru/dashboard/50158) в виджете "Текущий релиз (dna/web/perl)"
2. Получает аппрув на хотфикс у [sonch@](https://staff.yandex-team.ru/sonch) и [collapsus@](https://staff.yandex-team.ru/collapsus)

**Разработчик задачи, требующей хотфикса:**
1. Мержит фикс в транк
2. Делает cherry-pick своих коммитов в релизные бранчи затронутых приложений

**Дежурный тестировщик:**
1. Пушит исправление дежурным разработчиком критичных багов, найденных при тестировании, некритичные баги отцепляет от релиза
2. Докатывает хотфиксы, срочность которых обосновал менеджер в релизном тикете и которые окнули [sonch@](https://staff.yandex-team.ru/sonch) и [collapsus@](https://staff.yandex-team.ru/collapsus)

### Выкладка релиза
**Дежурный тестировщик:**
1. Когда тестирование завершено, регрессия разобрана, все найденные баги исправлены или признаны некритичными - отписывается в релизный тикет [комментарием](https://st.yandex-team.ru/settings/templates/comments?name=Релизный%20коммент&owner=1120000000006354&queue=DIRECT) и переводит релизный тикет в статус `RM Acceptance` нажатием на кнопку `Passed`
2. В окна выкладки робот попросит выложить релиз автоматически. Отслеживать просьбы робота и реакцию дежурных можно в [чате]({{chat-direct-admin}})


### Хотфиксы в прод
**Менеджер задачи, требующей хотфикса:**
1. Пишет обоснование необходимости хотфикса своей задачи [по шаблону](https://st.yandex-team.ru/settings/templates/comments?name=hotfix%20approve%20comment&owner=1120000000014295&queue=DIRECT) в последний выкаченный в прод релизный тикет нужного приложения: dna, java-web, perl. Найти релизный тикет можно [по фильтру](https://st.yandex-team.ru/issues/?_f=type+priority+key+summary+description+status+resolution+updated+assignee+parent&_q=Queue%3A+DIRECT+AND+Type%3A+Release+AND+Status%3A+Closed+AND+%28Components%3A+%22App%3A+dna%22+OR+Components%3A+%22App%3A+java_web%22+OR+Components%3A+%22Releases%3A+Direct%22+%29)
2. Получает аппрув на хотфикс у [sonch@](https://staff.yandex-team.ru/sonch) и [collapsus@](https://staff.yandex-team.ru/collapsus)
3. Предупреждает дежурного тестировщика и app-duty о планируемом хотфиксе в прод

**Разработчик задачи, требующей хотфикса:**
1. Мержит фикс в транк
2. Делает cherry-pick своих коммитов в релизный бранч с версией прода для всех затронутых приложений, а так же во все более поздние релизные ветки   
Найти релизный тикет последнего выкаченного в прод релиза можно [по фильтру](https://st.yandex-team.ru/issues/?_f=type+priority+key+summary+description+status+resolution+updated+assignee+parent&_q=Queue%3A+DIRECT+AND+Type%3A+Release+AND+Status%3A+Closed+AND+%28Components%3A+%22App%3A+dna%22+OR+Components%3A+%22App%3A+java_web%22+OR+Components%3A+%22Releases%3A+Direct%22+%29).   
Актуальные релизы можно увидеть [на дашборде](https://st.yandex-team.ru/dashboard/50158)

**Тестировщик задачи, требующей хотфикса:**
1. Тестирует фикс в ветке
2. Контролирует и пушит процесс с фиксом и выкладкой хотфикса на ТС и в прод
3. Тестирует фикс на ТС

**Дежурный тестировщик:**
1. Собирает хотфиксы, срочность которых обосновал менеджер в релизном тикете и которые окнули [sonch@](https://staff.yandex-team.ru/sonch) и [collapsus@](https://staff.yandex-team.ru/collapsus)
2. Обновляет тестовые среды: ТС и релизные беты (8999, 14601)
3. Заправшивает выкладку в прод у админов
