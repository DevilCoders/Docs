**Stater project**

**About project:** 
Yet another statistic module
**methods**:
- POST http request 
- routine (week day is passed by BATCHDAY env variable)
**routes**:
POST /st_stat (detailed monthly statistics for incident response times and fullfilment of tickets )
json data fields(not requiered):
date - start date for stat
offset - offset in monthes

POST /release_stat (statics for release  tickets in SEARCHMON metaqueue)
json data fields(not requiered):
date - start date for stat
offset - offset in monthes

POST /juggler_stat (daily juggler statistic for notification to robot-searchmon recepient)

POST /customjson (custom json data loader to statface)
json data fields: any valid statface json

POST /test_ststat (incidents created for period in days(daily metric))
 
*oauth token header and membership in marty owners group required for http request.
