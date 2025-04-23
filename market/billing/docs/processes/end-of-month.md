# Конец месяца

## Порядок работы

1. В течении всего месяца собираем проблемы будут мешать закрывать текущий месяц;
2. Для этого в начале месяца делаем тикет на закрытие <https://st.yandex-team.ru/createTicket?queue=MARKETBILLING&components=95645>
3. За неделю до конца месяца доделываем экстренно по плану
4. 1-го числа сообщаем большому Биллингу, что от нас все данные в порядке (TODO: уточнить как сообщаем (тикет?) и что делаем, если с нашей стороны данные задерживаются)
5. 2-3-го числа, когда все экстренное сделали, проводим ретроспективу и планируем, что надо доделать до конца следующего месяца

## Чеклист закрытия месяца

Чтобы закрытие месяца посчитать успешным, надо проверить следующее:

1. В тикете на закрытие месяца все пункты закрыты в "зелёный" статус или не мешают закрытию месяца (нужно чекнуть об ответственных)
2. Проверить даты последнего запуска джоб обилливания [скрипт проверки](https://a.yandex-team.ru/arc_vcs/market/billing/infra/diagnostics/end-of-month/bill-results-completeness.sh)
3. Проверить, что все обиленные услуги собрались в tlog [скрипт проверки](https://a.yandex-team.ru/arc_vcs/market/billing/infra/diagnostics/end-of-month/tlog-collected.sh) и [график](https://solomon.yandex-team.ru/?project=market-billing&cluster=agent-metrics&service=market-billing-tms&l.sensor=not_exported_to_tlog_transactions.count.*&graph=auto&l.host=*)
4. Проверить, что все обилленные международные услуги собрались в tlog
5. Проверить, что начисления по 610 и 609 сервисам собрались в tlog'и
6. Проверить, что все tlog'и экспортированы в YT [скрипт проверки](https://a.yandex-team.ru/arc_vcs/market/billing/infra/diagnostics/end-of-month/tlog-exported.sh)
7. TODO: Сообщить о готовности в Баланс и получить отмашку, когда Баланс забрал tlog'и
8. Акты по 609 сервису сходятся с отчетом Платежи и отчетом Заказы
9. Отчет по реализации товаров уехал в OEBS (на это есть 5 рабочих дней после первого числа)
10. АВ посчиталось и сошлось с Отчетом Агента (формируется в OEBS к 9-ому числу)
11. Отчет Агента (формируется в OEBS к 9-ому числу) сходится с отчетом Платежи и отчетом Заказы

## Ссылки { #links }

* Инструкция по закрытию: <https://docs.yandex-team.ru/market-billing/ops/guide/end-of-month-diag>
* Таблица большого Биллинга: <https://wiki.yandex-team.ru/users/bali7/reglament-zakrytija-po-servisam/>
* Регламент информирования о проблемах Маркет-Биллинга (черновик): <https://wiki.yandex-team.ru/users/teslenko/informirovannie-o-problemax-billinga/>
* Закрытие международного биллинга: <https://wiki.yandex-team.ru/users/pavel-repin/zakrytie-mesyaca-global-billing-israel/>
