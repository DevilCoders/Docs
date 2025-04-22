# Golovan alerts and panels for RTC

Supported entities:
* [alerts/manual](https://wiki.yandex-team.ru/golovan/alerts/)
* [alerts/templated](https://wiki.yandex-team.ru/golovan/templatium/napisanie-shablonov-alertov/)
* [panels](https://wiki.yandex-team.ru/golovan/templatium/writing/)
* [trees](https://wiki.yandex-team.ru/golovan/menutreeapi/)

# Cron

**All changes in Golovan will be overwritten, beware!**

Golovan will be periodically updated with https://sandbox.yandex-team.ru/scheduler/15740/view.

# HOWTO

## How to upload configuration

    1. ya make -r
    2. change templates
    3. ./updater --dry-run |& less # to see desired changes
    4. svn ci -m 'updated alerts'
