db
==

* `fill_admin_permissions.py` - assign admin permissions to groups defined in
                                `grant_access_to_admin_and_cabinet.py`

* `fill_exam_score.py` - fill exam bonus scores in `cities` collection.

* `grant_access_to_admin_and_cabinet.py` - grant access to admin and cabinet
                                           for selected users.

* `grant_access_to_exams.py` - grant access to exams.

* `fix_driver_licenses.py` - fix driver licences.

* `fix_driver_statistics.py` - remove driver from all unique_drivers docs
                               where driver license not in licenses list.

* `antifraud_config.py` - antifraud configuration.

* `manage_email_templates` - tool to manage email templates in db.static.

* `promotions_config.py` - config for `TeslaPromoHandler`

* `send_feedback_to_otrs.py` - re-submit order feedback we missed during
                               TAXIBACKEND-2520 roll-out.

* `fill_geoobjareas.py` - fill dbtaxi.geoobjareas from dbtaxi.cities

* `fill_geoobjsuggplaces.py` - fill places for suggesteddestinations

* `park_offer_contracts.py` - dump park offer contracts and corresponding cities.

* `chargeback.py` - handle chargeback

* `expman.py` - extend experiment with phone number

* `manage_mystery_shoppers.py` - add/remove/show phone numbers in mystery shoppers list

* `mystery_shopper_mark_drivers_passed.py` - mark drivers as passed mystery shopper
