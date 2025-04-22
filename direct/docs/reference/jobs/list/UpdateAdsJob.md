### Продукт/подсистема

Мастер кампаний.

### Роль в работе продукта/подсистемы

Джоба асинхронно создает/обновляет баннера,
группы и условия показа для UC (ТГО) и UAC (РМП).<br/>
Основная цель - синхронизация данных по баннерам из YDB/Grut в MySQL, для переданной кампании.

### Датафлоу

1) Джоба ходит в [YDB базу](https://ydb.yandex-team.ru/db/ydb-ru/mobileproducts/prod/rmp/browser) или в Grut в [man](https://yt.yandex-team.ru/seneca-man/navigation?path=//home/grut/stable/db), [sas](https://yt.yandex-team.ru/seneca-sas/navigation?path=//home/grut/stable/db), [vla](https://yt.yandex-team.ru/seneca-vla/navigation?path=//home/grut/stable/db), [markov](https://yt.yandex-team.ru/markov/navigation?path=//home/grut/stable/db)
   для получения необходимых данных (кампания, ее контенты)
2) Подчищает MySQL-баннера для удаленных YDB/Grut-контентов (останавливает, а затем архивирует/удаляет)
3) Создает новые или обновляет существующие баннера, группы и условия показа в MySQL по данным из YDB/Grut
4) Обновляет у контентов в YDB/Grut статусы, причины отклонения и флаги кампании

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.UpdateAdsJob.working.production&last=1DAY&query=)
- [Логи](https://direct.yandex.ru/logviewer/short/v2/1194774545173500634)

### Какая функциональность пострадает от отказа джобы

Не будут создаваться и обновляться баннера, группы и условия показа для кампаний,
созданных через Мастер кампаний.

### Как пользователи (или команда) заметят проблему и через какое время

Создание и обновление кампаний через интерфейс Мастера кампаний будет проходить без ошибок,
но пользователи будут видеть, что их кампания долго находится в статусе
"На модерации" или "Обрабатывается".

### Контакты разработчиков и менеджеров

Разработчики: [@khuzinazat](https://staff.yandex-team.ru/khuzinazat)
[@dimitrovsd](https://staff.yandex-team.ru/dimitrovsd)
[@bratgrim](https://staff.yandex-team.ru/bratgrim) <br/>
Менеджеры: [@anyksenya](https://staff.yandex-team.ru/anyksenya)

### Желательное время исправления в случае поломки

Максимально быстро.

### Способы регулирования работы джобы

Способ исправления последствий отказа джобы:
- положить список кампаний в очередь для обработки джобой через
[внутренний отчет](https://direct.yandex.ru/internal_tools/#update_ads_deferred_tool).
Выполняется под супером.
- Выполнить ваншот [uc.UacUpdateAdsOneshot](https://a.yandex-team.ru/arc_vcs/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/oneshots/uc/UacUpdateAdsOneshot.kt?rev=r8798285#L1) с указанием пути к yt табличке со списком id кампаний. [Пример запуска](https://direct.yandex.ru/internal_tools/#oneshot_launches) №1117

### Известные причины поломок

Выход в прод использования в коде нового поля из таблиц YDB/Grut до применения миграции в проде.

### Дополнительно: тонкости и подводные камни

В случае ошибок делается 2 отложенных рестарта джобы, каждый через 20 минут.
