# Отчет стоимость услуг/услуги маркетплейса (UnitedMarketplaceServicesXlsGenerator)

## Виды отчета

Отчет заказывается по [услугам синего биллинга](https://docs.yandex-team.ru/market-billing/reference/tlog#uslugi-sinego-billinga) из партнерки в двух форматах:
1. **Отчет дате начисления услуги** - отчет содержит информацию об услугах за выбранный интервал дат.
2. **Отчет дате формирования акта** - отчет содержит информацию об услугах, попавших в акты за выбранные месяцы.

**Особенности:**
* В отчет по актам **не входит** информация о взаимозачетах за долги маркета партнеру, потому отчет все равно может не сходится
   с актами баланса.
* `TODO: написать про взаимозачет и в будущем сослаться здесь на описания взаимозачетов`
* Отчет по актам может содержать **катоффы**(услуги из прошлого месяца, занесенный в акт следующего по разным причинам) за 10 дней до начала месяца. Количество дней прописано [здесь](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/united/services/generator/UnitedMarketplaceYtDao.java?rev=r9551517#L46).


## Как устроен
Логика работы отчета делится глобально на две части - сбор данных и построение отчета.

### Сбор данных
Выполняется в компоненте `market-billing-tms`.
Данные собираются джобой [transactionReportLogYtExportExecutor](https://docs.yandex-team.ru/market-billing/reference/jobs/list/transactionReportLogYtExportExecutor).
Джоба раз в полчаса читает данные транзакционного лога, начиная с последней выгруженной транзакции, обогащает их информацией для отчета в поле `payload2` и выгружает их
в [папку на YT](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/market/production/mbi/billing/tlog-report/revenues).

**Особенности:**
* Информация на YT хранится в папках с именем даты услуги `event_time`, чем и отличается от обычной выгрузки транзакционного лога, хранящего записи в таблицах с датой из `transaction_time`.  Так сделано для удобства построения отчетов.
* Особую роль играет то, что мапперы преобразований поля `market_billing.transaction_log.key` строго заданы. Потому, при добавлении новой услуги или
изменении первичного ключа старой услуги в [конфиге сбора тлога](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlog/config/TransactionLogConfig.java?rev=r9532378#L312),
обязательно надо править или добавлять мапперы в соответствующей [папке](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlogreport/marketplace/mappers/).
* Папок выгрузок две `revenues` и `revenues-copy` на случай изменения данных и перезаливки записей тлога с нуля. Подробнее в документации джобы по ссылке выше.
* При изменении типа выгружаемых значений в `...Payload2Dto-классах`, необходимо поменять `...Payload2Dto-классы` для корректного маппинга значений тлога в [соответствующей папке монолита](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/services/payload2/?rev=r9369113)

### Построение отчета
Выполняется в компоненте `mbi-report-generator`.
1. Бизнес выбирает тип отчета и временной интервал в `Бухгалтерия->Стоимость услуг` [ЛК ПИ](https://partner.market.yandex.ru/).
2. Формируется запрос, который отправляется в табличку монолита `shops_web.async_reports`.
3. Воркер читает табличку и по типу отчета переходит в [UnitedMarketplaceServicesFileReportGenerator](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/united/services/UnitedMarketplaceServicesFileReportGenerator.java?rev=r9534230#L52).
Если дата с которой формируется отчет раньше `01.09.2021`, то отчет формируется по Oracle по старой логике. В противном случае используется новая логика.
4. Начинаем выполнять основной метод генерации: [generateFromPayload2](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/united/services/generator/UnitedMarketplaceFromYtXlsGenerator.java?rev=r9414560#L135)
   1. Получаем информацию о партнерах, для которых запрошен отчет из переданных фронтом параметров [createHeadersFromParams](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/united/services/generator/UnitedMarketplaceYtDao.java?rev=r9551517#L374).
   Выбираются только партнеры, договор которых находится в статусе [COMPLETED](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/mbi-model/src/main/java/ru/yandex/market/core/application/PartnerApplicationStatus.java?rev=r8570582#L42)
   2. Формируем параметры для запроса выбранного типа отчетов и забираем данные об актах и последних транзакциях для интервала дат отчета [getActsWithLastTransactionIds](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/united/services/generator/UnitedMarketplaceYtDao.java?rev=r9551517#L337)
   3. Выполняем [getPayload2queryExecute](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/united/services/generator/UnitedMarketplaceYtDao.java?rev=r9551517#L271), забирая строки для генерации из собранных на YT данных и маппим `payload2` с помощью
   [PRODUCTS_MAP](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/united/services/generator/UnitedMarketplaceFromYtXlsGenerator.java?#L99). Здесь же проставляем строке дату акта, в которой она забрана с помощью [setActDateToPayload2Dto](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/united/services/generator/UnitedMarketplaceYtDao.java?rev=r9551517#L313).
   4. Строки группируются для транзакций, связанных посредством `previous_transaction_id` с помощью [groupPreviousTransactions](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/united/services/generator/UnitedMarketplaceFromYtXlsGenerator.java?rev=r9414560#L197)
   5. Для получившихся значений [формируем листы по каждой услуге](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/united/services/generator/UnitedMarketplaceFromYtXlsGenerator.java?rev=r9414560#L152) и выгружаем отчет.

**Особенности**
* Каждый лист формируется по-своему со своей сортировкой и иногда группировкой. Для части листов нужны информации о регионах, которые берутся из `shops_web.regions`. Для листа с хранением используются походы в [MBO](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/united/services/generator/UnitedMarketplaceFromYtXlsGenerator.java?rev=r9414560#L509).
  Вспомогательные методы описаны в [UnitedMarketplaceFromYtService](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/united/services/generator/UnitedMarketplaceFromYtService.java?#L32)
* При добавлении нового продукта (=новой услуги для партнеров(=новая константа в [ProductId](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/model/billing/ProductId.java?#L10)))
  обязательно надо пополнить статическую переменную [PRODUCTS_MAP](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/united/services/generator/UnitedMarketplaceFromYtXlsGenerator.java?#L99)
* При проставлении даты акта, если акта на услугу еще нет(текущий месяц), проставляется `N/A`
* При походах в YT используется отдельный пул запросов [market-billing-reports](https://yt.yandex-team.ru/hahn/scheduling/overview?pool=market-billing-reports&tree=physical).
* При формировании отчетов может использоваться альтернативная папка с данными `revenues-copy`. За это отвечает env-переменная [USE_ALTER_PATH](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/report-generator/src/java/ru/yandex/market/rg/asyncreport/united/services/generator/UnitedMarketplaceYtDao.java?rev=r9551517#L41)
