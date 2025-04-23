Some not addressed issues that can hurt later:
---------------------------

## General 
- **ALERTING!**
- performance: Orders' service has problem of n+1 queries. Also, a lot can be done in parallel. *There was an idea not to put too much pressure on orders, therefore, probably orders' performance should be addressed first.*


### Spring Batch
- archiving or purging the metainfo about results of old jobs (spring batch tables)
- it seems like by default spring batch doesn't have indexes in their ddl (https://docs.spring.io/spring-batch/docs/current/reference/html/index-single.html#recommendationsForIndexingMetaDataTables)...
  *doesn't hurt ATM, but would be nice to check*
- Repeat/Retry job... didn't quite grasp the idea, need to re-check and write tests maybe...

