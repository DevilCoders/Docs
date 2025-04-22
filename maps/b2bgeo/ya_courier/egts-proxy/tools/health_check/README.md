# Testing position sending to an EGTS server

Use the binary ./health_check to test that an EGTS server receives positions and responds correctly and promptly.

To compile the binary:

    ya make -r

For the list of supported command-line options run:

    ./health_check --help

#### Test an EGTS server in the test environment

Run the check:

    ./health_check --host egts-test.yandex.net

#### Test an EGTS server in the production environment

Run the check:

    ./health_check --host egts.yandex.net

#### Test a local EGTS server

To test locally you should launch a local EGTS server first (it is located
two folders up the tree, in arcadia/maps/b2bgeo/ya_courier/egts-proxy).

Compile the server by 'ya make -r'.

Before launching the server make sure that you have set
YA_COURIER_BACKEND_OAUTH_KEY (you can find the value at
https://wiki.yandex-team.ru/b2bgeo/dev/robots/, 'robots-egts' row).

Launching the server:

    YA_COURIER_BACKEND_URL="https://test.courier.yandex.ru" \
    YA_COURIER_EXPIRE_DAYS="3650" \
    YCR_MODE="http:9090" \
    PG_HOST="man-t16k5yyubdv7q0pz.db.yandex.net,sas-lsgpofrwqk1nc7lw.db.yandex.net,vla-f35kg5u7sl6kurfk.db.yandex.net" \
    PG_PORT="6432" \
    PG_ARGS="dbname=b2bgeo_egts_test user=dbuser password=Ohhee2ah" \
    ../../egts-proxy --server --port 4000

Run the check:

    ./health_check
