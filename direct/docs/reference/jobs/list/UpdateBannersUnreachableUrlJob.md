## UpdateBannersUnreachableUrlJob

### Продукт/подсистема

[Внутренняя реклама (aka Банана)](../../../glossary/glossary.md#internal-ads).


### Роль в работе продукта/подсистемы

Аналог URL-мониторинга в большом Директе, но простукивает урлы целиком, а не только домен. Джоба останавливает объявления, у которых есть недоступные урлы.


### Датафлоу

- Вычитывает недоступные урлы из таблицы в YT [//home/yabs/banana/WrongDirectLinks](https://yt.yandex-team.ru/hahn/navigation?navmode=acl&path=//home/yabs/banana/WrongDirectLinks). Сама таблица заполняется [sandbox-таской](https://sandbox.yandex-team.ru/scheduler/8503/view) из старой бананы [подробнее на вики](https://wiki.yandex-team.ru/adv-interfaces/direct/banana/#validacijassylok). В будущем это поменяется и скорей всего будет другая джоба заполнять эту таблицу или все будет будет по-другому.
- Перепроверяет (простукивает) выгруженные (=проблемные) ссылки через Зору
- Останавливает те баннеры, у которых урлы все еще недоступны.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.UpdateBannersUnreachableUrlJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/short/eOthaNXV3o2z7V) (не забудьте исправить даты!)


### Какая функциональность пострадает от отказа джобы

Будут показы по баннерам с недоступными урлами.


### Как пользователи (или команда) заметят проблему и через какое время

Пока никак. Джоба будет дорабатываться и улучшаться в рамках [DIRECT-95847](https://st.yandex-team.ru/DIRECT-95847).


### Контакты разработчиков и менеджеров

Разработчики: [Александр Сластин](https://staff.yandex-team.ru/aslastin), [Бехруз Афзали](https://staff.yandex-team.ru/xy6er), [Захар Зибаров](https://staff.yandex-team.ru/zakhar) <br/>
Менеджеры: [Ваня Пахомов](https://staff.yandex-team.ru/irpakhomov), [Марина Ежова](https://staff.yandex-team.ru/ezhova-m)


### Желательное время исправления в случае поломки

В течении дня.


### Способы регулирования работы джобы

Отсутствуют.


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Отсутствуют.
