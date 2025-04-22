# Супер дока по всем-всем юнитам, с тэгом #partner_units_doc

{{ToC from=h1 to=h2}}
Просто мегатекст, 666 – the number of the beast

Sphinx is a *documentation generator* or a tool that translates a set of plain
text source files into various output formats, automatically producing
cross-references, indices, etc.  That is, if you have a directory containing a
bunch of xxx or yyy
documents, Sphinx can generate a series of HTML files, a PDF file (via LaTeX),
man pages and much more.

# Юниты:

## balance.thirdparty_transaction.OrderRewardUnit


### class balance.thirdparty_transaction.OrderRewardUnit(use_min_reward=True, required_comm_category=False, no_reward_paytypes=None, fair_order_reward=False, fair_ignored_fee=None, commission_category_from_incoming_row_field=None, \*\*kwargs)
Конфигурирование модуля расчета АВ. Для фиксированных схем используется юнит `balance.thirdparty_transaction.RewardUnit`, для схем, в которых процент зависит от логики сервиса и передается сервисом в качестве **commission_category**, используется `balance.thirdparty_transaction.OrderRewardUnit`


* **Параметры**


* **use_min_reward** (*bool**, **опционально*) – аналогично `balance.thirdparty_transaction.RewardUnit`


* **required_comm_category** (*bool**, **опционально*) – строго необходимо, чтобы значение категории комиссии было заполнено, транзакции в которых не заполнено, упадут в ошибку, если False - то с таких транзакций АВ не рассчитывается


* **no_reward_paytypes** (*list**[**int**]**, **опционально*) – аналогично `balance.thirdparty_transaction.RewardUnit`


* **fair_ignored_fee** (*list**[**int**]**, **опционально*) – список значений service_fee траста, с которых вознаграждение не рассчитывается, по умолчанию не задано


* **commission_category_from_incoming_row_field** (*str**, **опционально*) – задать атрибут исходной транзакции, содержащий категорию комиссии (только для YT), по умолчанию не задано


## balance.thirdparty_transaction.RewardUnit


### class balance.thirdparty_transaction.RewardUnit(use_min_reward=True, min_reward_value=None, no_reward_paytypes=None, use_min_reward_by_currency=True, reward_from_incoming_row_field=None, reward_is_amount=False, reward_from_partner_commission_sum=False, reward_is_pct_of_amount=False, reward_pct=None, reward_pct_from_partner_commission_pct=False, reward_pct_from_partner_commission_pct2=False, reward_pct_from_medicine_pay_commission=False, zero_reward_for_zero_pct=False, zero_reward_is_null=False, add_nds_firms=None)
Конфигурирование модуля расчета АВ. Для фиксированных схем используется юнит `balance.thirdparty_transaction.RewardUnit`, для схем, в которых процент зависит от логики сервиса и передается сервисом в качестве **commission_category**, используется `balance.thirdparty_transaction.OrderRewardUnit`


* **Параметры**


* **use_min_reward** (*bool**, **опционально*) – включить логику применения «минималки» для АВ, по умолчанию True


* **min_reward_value** (*decimal**, **опционально*) – если задано, определяет значение минимального размера АВ, по умолчанию выключено


* **no_reward_paytypes** (*list**[**int**]**, **опционально*) – список методов оплаты, с которых АВ не рассчитывается, по умолчанию не задано


* **use_min_reward_by_currency** (*bool**, **опционально*) – включить логику применения «минималки» по валюте транзакции (0.01 для RUB, 15 Тенге для KZT), менее приоритетно чем **use_min_reward**, по умолчанию False


* **reward_from_incoming_row_field** (*str**, **опционально*) – определяет атрибут входящей транзакции для базы АВ (только для YT)


* **reward_is_amount** (*bool**, **опционально*) – является ли вознаграждением вся сумма строки транзакции, по умолчанию False


* **reward_from_partner_commission_sum** (*bool**, **опционально*) – использовать ли фиксированный размер вознаграждения с транзакции, заданный в договоре, по умолчанию False


* **reward_is_pct_of_amount** (*bool**, **опционально*) – вознаграждение рассчитывается по принципу взятия процента от суммы транзакции, источник процента определяется следующими параметрами, по умолчанию False


* **reward_pct** (*decimal**, **опционально*) – процент агентского вознаграждения константой конфига, по умолчанию не задано


* **reward_pct_from_partner_commission_pct** (*bool**, **опционально*) – используется ли атрибут договора *partner_commission_pct* в качестве процента АВ, по умолчанию False


* **reward_pct_from_partner_commission_pct2** (*bool**, **опционально*) – используется ли атрибут договора *partner_commission_pct2* в качестве процента АВ, по умолчанию False


* **zero_reward_for_zero_pct** (*bool**, **опционально*) – не брать минималку при нулевом проценте АВ, по умолчанию False


* **add_nds_firms** – **TODO**
