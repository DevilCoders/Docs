# Boro Alerts

Elecard Boro -> Juggler  
Simple webservice that proxies alerts from http://boro.strm.yandex.net to juggler.  
Uses: PGASS (state), Redis (distributed alerts)

API: https://strmticket.yandex-team.ru/boro/docs  

Service: https://deploy.yandex-team.ru/stages/boro-alerts-prod  

CI: https://a.yandex-team.ru/ci/boroalerts/releases/timeline

Raw juggler events: [here](https://juggler.yandex-team.ru/raw_events/?query=host%3Dsas3-9342-1.y5wehmogyxuwdvh4.sas.yp-c.yandex.net%7Chost%3Dvla0-6649-1.lajmdgqlqaajhwdz.vla.yp-c.yandex.net&limit=120)
