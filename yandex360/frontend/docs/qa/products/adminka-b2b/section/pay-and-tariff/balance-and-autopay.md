# Структура блока с балансом и автосписанием


{% note info "Важное про постоплату" %}

Для постоплатников данный блок отсутствует (у них нет баланса и, соответственно, предельной даты)

Вместо этого у них отображается плашка с текстом "Счет будет выставлен..."

{% endnote %}

## баланс и дата "хватит до..."

Блок отображает сколько сейчас денег на счету и до какого числа их хватит (если подключен какой-либо тариф)

Дата "Хватит до..." рассчитывается на бэкенде и зависит от:
* количества организаций плательщика с платными тарифами
* количества пользователей в каждой организации с подключенным платным тарифом

{% note info "Про минус на балансе:" %}

Минуса на предоплате (только если пользователь не переехал с постоплаты) не может быть - если мы понимаем, что у пользователя текущих средств на балансе не хватит на 1 день, то отключаем его от платного тарифа

{% endnote %}

## автосписание

Пользователь может управлять автосписанием - активировать, приостанавливать, менять активные карты

**По дефолту автосписание активно**
