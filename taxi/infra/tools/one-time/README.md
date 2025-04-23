One-time scripts
================

* `audi_a6.py` - find all active AUdi A6 in Moscow parks.

* `spb_polygons.py` - calculates trip statistics in two areas of
                      Saint-Petersburg (TAXIBACKEND-1803).
* `send_sms_spb_unified.py` - notifies Saint-Petersburg drivers about
                              profile unification (TAXIBACKEND-1859).
* `spb_car_dist.py` - builds per class distributions for the last
                      month' active cars in Saint-Petersburg
                      (TAXIBACKEND-1805).
* `phone_orders.py` - checks if there were any orders for given
                      phone numbers in last 45 days (TAXIBACKEND-1824).
* `no_cost.py` - finds completed orders that have no cost data in the
                 give date range. Moscow-only (TAXIBACKEND-1836).

* `parks_without_waiting_to_airport.py` - finds all parks without
                                          `waiting_to_airport` field.

* `park_ids.py` - prints clid to datasource_id mapping as well as some
                  other park info.

* `deptrans` - calculate stats for deptrans and create heatmaps.

* `mqc_check_interval.py` - change MQC check interval to one year.

* `calc_vs_cost.py` - statistics on difference between real and
                      calculated costs.
* `update_golds_collection.py` - sets GOLD status to cars from the
                                 given CSV file (TAXIBACKEND-2087).

* `generate_classification_rules.py` - updates classification rules
      format, which allows concurrent existence of two versions of
      classification tasks.

* `rebill_orders.py` - unset `billing` field in all orders during
      specified period.

* `incorrectly_billed.py` - fetch orders with billing issues.
      Details are in https://otrs.yandex-team.ru/~31282125/.

* `requestcar_vs_carack.py` - calculate requestcar/carack statistics
      to help us decide if drivers are reluctant to take card orders.

* `generate_promocodes.py` - generate vast amount of promocodes for
      marketing team (TAXIBACKEND-2270).
      
* `testing_parks.py` - recreate billing IDs for parks in testing after
      billing team deleted its database.
      
* `16417-fix_orders_with_hold_tiny_sym.py` - fix old orders, there transactions 
      has little bit less sum_to_pay than origin
