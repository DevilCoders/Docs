# referralYtImportExecutor

### Код
Основной код:
[ReferralYtImportExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/distribution/yt/ReferralYtImportExecutor.java),
[ReferralYtImportService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/distribution/yt/ReferralYtImportService.java),
[DistributionReferralDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/distribution/dao/DistributionReferralDao.java),

### Продукт/подсистема

Импорт с YT партнеров Дистрибуции - участников B2B реферальной программы

### Роль в работе продукта/подсистемы

Джоба импортирует данные о реферерах и рефералах

### Датафлоу

Джоба читает данные с кластера Hahn на yt.
Путь до таблицы в проде: `mbi.distribution.referrals.yt.import.path=//home/distribution-statistics/market/referrals`
Таблица в billing pg: market_billing.distribution_referrals
Таблица на YT читается целиком, исчезнувшие записи о рефералах удаляются из базы (в нормальном флоу они не должны
исчезать, но могут в случае ошибочной записи в источнике), остальные записываются через upsert.

### Способы наблюдения за текущим состоянием
- Мониторинг Juggler

### Какая функциональность пострадает от отказа джобы

Данные о новых рефералах перестанут сохраняться в базе. В результате не будет посчитано вознаграждение партнерам
по реферальной программе - данные о заказах рефералов не попадут ни в Баланс, ни в статистику.

Поскольку стандартное время до подтверждения первых заказов по партнерской программе 14 дней,
задержка с поставкой данных о рефералах на пару дней не должна повлиять на выплаты.

### Как пользователи (или команда) заметят проблему и через какое время

По мониторингам

### Контакты разработчиков и менеджеров
[ABC-группа market-affiliate] (https://abc.yandex-team.ru/services/market-affiliate/) <br/>

### Желательное время исправления в случае поломки

3-4 дня

### Способы регулирования работы джобы

### Известные причины поломок

### Дополнительно: тонкости и подводные камни