# How to import users from arm1.0

ssh jams-arm-dbs01h.maps.yandex-team.ru

echo 'select user_id, login, blocked, role, region_box, user_uri from users;' | mysql -u arm-read -h localhost -D jams_arm_partner -p****** | tail -n +2 | sed "s/'/\'/;s/\t/\",\"/g;s/^/\"/;s/$/\"/;s/\n//g" | tee users.csv

> bring users.csv here

python main.py  users.csv | tee points_users.sql

cat points_users.sql | psql 'user=arm password=******* host=pgaas-test.mail.yandex.net port=12000 dbname=maps_core_jams_arm_testing'