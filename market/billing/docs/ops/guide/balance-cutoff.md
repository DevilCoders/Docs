# Как проверить катофф баланса

### Что такое катофф баланса?
От английского слова **cutoff** - _отсекать_.
Транзакции которые были сделаны в прошлом месяце, но не попали (отсечены от) в акт об исполнени услуг прошлого месяца...
Они войдут в акт следующего месяца.

### Почему это проблема?
То что не добавилось в текущем акте, будет добавлено в следующем, и будет превышать ожидания и расстроит партнера.

### Как посмотреть катофы?
Катофы можно посмотреть с помощью запроса в Ыте.


``` sql
USE hahn; PRAGMA yt.pool = "market-billing-reports";
$partnerContractInfo = "//home/market/production/mbi/partner_stats/partner_contract_info";
$balanceActs = "//home/market/production/mbi/billing/balance/revenue_tlog_acts_timeline";

$dateFrom = "2022-06-01";
$dateTo = "2022-07-01";

$checkDateFrom = "2022-07-01";
$checkDateTo = "2022-07-05";

select tlog.*
from $partnerContractInfo as pci
join $balanceActs as acts on acts.contract_id = pci.income_contract_id
join range(`home/market/production/mbi/billing/tlog/revenues/`,$checkDateFrom, $checkDateTo) as tlog on tlog.partner_id = pci.partner_id
WHERE
acts.act_dt between $dateFrom and $dateTo
and tlog.transaction_id > acts.last_transaction_id
and substring(tlog.event_time,0,10) = acts.act_dt;
```


В запросе в качестве примера приведен месяц Июнь.
Для того чтобы переписать на другой месяц надо поменять даты начала и конца месяца для акта - _**$dateFrom, $dateTo**_.
И даты проверки **_$checkDateFrom, $checkDateTo_** - первые пять дней начала следующего месяца.
