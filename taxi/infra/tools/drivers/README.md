Operations with drivers
=======================


Conflicts with licenses
-----------------------

`print_license_info.py` prints information about licenses.

`remove_profile_from_unique.py` removes redundunt profile from document
of `unique_drivers` collection.

`edit_unique_drivers_with_new_licenses.py` if driver change license,
merge new and old license in `unique_drivers` collection.

`insert_cars_into_permits_whitelist.py` is used for solving task
[TAXIBACKEND-2249](https://st.yandex-team.ru/TAXIBACKEND-2249). It appends
a single car to a list of cars, for which permits are not checked.

`manual_set_golds` is used for set golds state for drivers from file.
As gold grades are recalculated every night, this script should be run
every day too.
