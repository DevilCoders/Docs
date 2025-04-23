Install
====
cd ./nanny_jinja_tests;
ya make

Example
====
Обычный сервис (GENCFG)


./bin/njt --service ygetparam_new --port 15015 --instance vla1-0061.search.yandex.net --show-context -s ./test.tmpl -d ./result


YP_LITE


/bin/njt --service rtc_planned_work -i dt16o16b014gz.man.yp-c.yandex.net  -s ./template.conf -d ./result.conf


Переменные "заглушки"
====
К сожалению не все переменные можно дастать хоста, по этой причине некоторые из них были сделаны в виде заглушек.

BSCONFIG_IDIR & HOME - генерируется полностью локально. На реальной машине этот путь может отличаться.

ISS - Всегда "1"

BSCONFIG_SHARDDIR - Всегда "./". Deprecated.

BSCONFIG_SHARDNAME - Всегда пустой. Deprecated.

HQ_INSTANCE_SPEC_HASH - генерируется. UUID.

CONTAINER - Статично задан "porto".

container - Статично задан "lxc".

USER - статично задан "loadbase".

