## SendPushesJob

### Продукт/подсистема

Отправка пользователям сервер-пушей.


### Роль в работе продукта/подсистемы

Отправляет пуши пользователям через [сервис Xiva](https://console.push.yandex-team.ru/#),
забирая их из очереди [ppc.xiva_pushes_queue](https://direct-dev.yandex-team.ru/db/ppc/tables/xiva_pushes_queue.html).


### Датафлоу

- Достает пачку пушей из очереди [ppc.xiva_pushes_queue](https://direct-dev.yandex-team.ru/db/ppc/tables/xiva_pushes_queue.html)
- Отправляет их в [Xiva](https://console.push.yandex-team.ru/#)
- Удаляет пуши из очереди [ppc.xiva_pushes_queue](https://direct-dev.yandex-team.ru/db/ppc/tables/xiva_pushes_queue.html)


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.SendPushesJob.working.production&last=1DAY)
- [Xiva-логи](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/xivahub-log)
- [График по числу отправленный сообщений в реальном времени](https://yasm.yandex-team.ru/template/panel/xiva_main_panel/env=production;service=direct/26/)


### Какая функциональность пострадает от отказа джобы

Пуши не будут посылаться.


### Как пользователи (или команда) заметят проблему и через какое время

Данные в интерфейсе будут меняться только при обновлении страницы.

Не критично.


### Контакты разработчиков и менеджеров

Разработчики: [Мария Чухарева](https://staff.yandex-team.ru/mredor) <br/>
Менеджеры: [](https://staff.yandex-team.ru/)


### Желательное время исправления в случае поломки

?


### Способы регулирования работы джобы

?


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни
Пока джоба не работает, очередь растет. <br/>
Устаревшие пуши отправлять бессмысленно, так что очередь надо почистить.
(если не сделать это ручками, джоба сама почистит, но в это время не будет выполнять отправку)
