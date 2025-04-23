Skills Updater
==============

Skills Updater is a periodical task that recalculates active users skills.

'Active users' are users whos recent actions lead to moderation tasks creation and 'skills' are number of moderation tasks divided by categories and resolutions.

Currently `recent actions` are actions made _yesterday_. Therefore, two consequence running of the application will recalculate skills for the same users. However, that does not mean that the result will be the same, as these users might act inbetween executions.

Information is calculated about active users only as it is further used for feed filters (users without changes are not represented in the feeds) and for automatic granting and withdrawing permissions (non-active users has no urge in extended permissions).

The idea behind this application can be found on [wiki](https://wiki.yandex-team.ru/maps/dev/core/wikimap/avtomaticheskoe-vychislenie-jekspertizy).


Usage
-----
The application does not support any command line arguments, and must be executed as is.

For establishing connections towards the DB, configuration files from `maps/wikimap/mapspro/cfg/services` are used (by means of `maps/wikimap/mapspro/libs/common/include/yandex/maps/wiki/common/default_config.h`).
