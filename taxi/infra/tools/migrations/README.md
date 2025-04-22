Migrations of database scheme
=============================

1.8.59
------

  * set `payment_tech.antifraud_group_recalculated` in orders

1.8.52
------

  * set `performer.taxi_alias.id` in orders

1.8.48
------

  * update MAT in parks

1.8.33
------

  * add `billing.rrn`, `billing.status_code`, `billing.status_desc` to
    `db.user_invoice_transactions` collection

1.8.31
------

  * add `transaction.type` to `db.user_invoice_transactions` collection
    [TAXIBACKEND-2022](https://st.yandex-team.ru/TAXIBACKEND-2022)
  * add `pending_refunds` field to `db.user_invoices` collection
    [TAXIBACKEND-2022](https://st.yandex-team.ru/TAXIBACKEND-2022)

1.8.26
------

  * set `taxi_alias_id` to `db.user_invoices` collection
    [TAXIBACKEND-1987](https://st.yandex-team.ru/TAXIBACKEND-1987)
  * `cards` and `billing_orders.0.card_id` in `user_invoices`
  * unset `card` and `billing_orders.0.card` in `user_invoices`
  * set `card_id` in `user_invoice_transactions`

m2233
-----

Add `exact_orders` boolean field (initially set to true) to `cities`
collection.

m2113
-----

Add `cities` field to `coupon_series` document so one can attach coupons
to cities.

m1965
-----

Adds field `city` to `dbtaxi.exams` and fills for every document of the
collection. Filling is based on `park` field. If park is missed sets
Moscow as default city.
