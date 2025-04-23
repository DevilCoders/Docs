# Stress testing position sending to an EGTS server

Use the binary ./stress_load to test that an EGTS server can receive lot of positions.

To compile the binary:

    ya make -r

Default values for the options are tuned down to prevent an unintented overload of the server, so please check the list of supported command-line options by

    ./stress_load --help

and set appropriate options to the values you want (e.g. -c 4000).

Note that you have to increase maximum number of the open files by launching 'ulimit -n XXXX' (where XXXX is the number).
It should be slightly bigger than the number of the clients specified by the -c option.

#### Test an EGTS server in the test environment

Run:

    ./stress_load --host egts-test.yandex.net -c 8000 -d 600 --min_send_interval 5 --max_send_interval 6


#### Test an EGTS server in the production environment

Run:

    ./stress_load --host egts.yandex.net -c 8000 -d 600 --min_send_interval 5 --max_send_interval 6

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
    ./egts-proxy --server --port 4000

Run the check:

    ./stress_load

#### Test a locally built server in testing env

    cd ~/arcadia/maps/b2bgeo/ya_courier/egts-proxy
    ya package maps-b2bgeo-ya-courier-egts-proxy.json

Note: substitute the real name of the generated file (.gz) in the command below:

    docker build --network=host - < maps-b2bgeo-ya-courier-egts-proxy.5131720.tar.gz

At the end of the ouput you will see something like 'Successfully built 5b440aa31e5d'

Use the id from the message in the following command ('registry.yandex.net/b2bgeo/egts:' part is from
the Repository item shown when you clcik [Update] at EGTS's docker box in QLoud Overview, and
load_testing is jsut a name you assign - feel free to use some other name but remeber it):

    docker tag 5b440aa31e5d registry.yandex.net/b2bgeo/egts:load_testing
    docker push registry.yandex.net/b2bgeo/egts:load_testing

On EGTS's docker box in QLoud Overview click [Update] , click Tags drop-down, select your build (by name, e.g. load_testing),
then click [Update]. Wait for deployment to complete, you're done.
