This document describes how Yandex.Taxi receives tracks and how to find a problem if there are no tracks from some partner.

## How it works

1. Partners of Yandex.Taxi send tracks according to [this NDA document][tracks-protocol] (note, **NDA!!**) to one of the following addresses:

  * http://extjams.maps.yandex.net/taxi_collect/1.x/ - in production
  * http://tst.extjams.maps.yandex.net/taxi_collect/1.x/ - in taxi-partners-test

2. Tracker after szubkovskij@ collects all of tracks.

3. Every 15 seconds Yandex.Taxi gets all tracks (last positions of tracks) from tracker.

All path from driver's device up to Yandex.Taxi takes 15-30 seconds (our part 1->3) plus time that depends on partner (we don't what time sending tracks to Yandex.Taxi takes).

## How to check whether Yandex.Taxi receives tracks or not

**In partner in production**: IP-address of host that sends tracks must be added to `backend-ip-config` package, and package must be installed and reloaded via conductor. In case of unknown IP-address parter gets 403 Forbidden error on attempts of sending tracks.

Information about all of tracks can be found at:

  * http://taxi-partners-test-tracks.mobile.yandex.net/getvehicles_internal (taxi-partners-test)
  * http://vehicles.mobile.yandex.net/getvehicles_internal (production)

If you don't see tracks from partner's clid then:

  * ask partner for HTTP answer code. If it's 403, look at [ip whitelist](Tracks#ip-whitelist) section
  * ask partner to check time of tracks (UTC)
  * ask szubkovskij@ to grep logs for specific clid
  * e-mail to khrolenko@, message must consists of: problem description, clid, logs from partner

Also you can see a number of online drivers in admin. But there are only correctly imported drivers.

[tracks-protocol]: http://doccenter.yandex-team.ru/en/jams/dg/yandex-maps-extjams-dg.pdf "How to upload GPS tracks"

## IP whitelist

Tracker receives tracks only from whitelisted ip addresses. List of those ip addresses is stored at [backend-ip-config](https://github.yandex-team.ru/taxi/backend-ip-config). There is a cron script after mkamalova@. It collects all partners ip adresses from production cabinet, push into repository, build package [yandex-maps-analyzer-auth-taxi-config](http://c.yandex-team.ru/packages/yandex-maps-analyzer-auth-taxi-config) and deploy this package to tracker servers.

So, if partner get 403 answer from tracker, you have to check his ip addresses in whitelist.