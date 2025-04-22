## auto-av-images-parser: 0.9.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-266: detect resellers with seller hash

## auto-av-images-parser: 0.8.7 (Mon, 23 Aug 2021 18:59:00 +0300)

 * detect resellers at night

## auto-av-images-parser: 0.8.6 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-262: check paths for exists and not empty

## auto-av-images-parser: 0.8.5 (Mon, 23 Aug 2021 18:59:00 +0300)

 * add all sellers to resellers kafka

## auto-av-images-parser: 0.8.4 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix logger import

## auto-av-images-parser: 0.8.3 (Mon, 23 Aug 2021 18:59:00 +0300)

 * change schedule for detect resellers

## auto-av-images-parser: 0.8.2 (Mon, 23 Aug 2021 18:59:00 +0300)

 * change schedule for detect resellers

## auto-av-images-parser: 0.8.1 (Mon, 23 Aug 2021 18:59:00 +0300)

 * change schedule for detect resellers

## auto-av-images-parser: 0.8.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-257: detect resellers job
 * VSEXTADAPROC-251: delete old tables
 * mdb kafka cluster

## auto-av-images-parser: 0.7.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-224: check nirvana instances in async manner
 * enforce limit for request queue query

## auto-av-images-parser: 0.6.4 (Mon, 23 Aug 2021 18:59:00 +0300)

 * use max day in to day in fill request queue yql query

## auto-av-images-parser: 0.6.3 (Mon, 23 Aug 2021 18:59:00 +0300)

 * limit amount of urls to process to 10kk (can't do more)
 * fix docker, use bionic

## auto-av-images-parser: 0.6.2 (Mon, 23 Aug 2021 18:59:00 +0300)

 * update dependencies

## auto-av-images-parser: 0.6.1 (Mon, 23 Aug 2021 18:59:00 +0300)

 * return in compare_meta

## auto-av-images-parser: 0.6.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-195: compare meta up to 100k rows at a time

## auto-av-images-parser: 0.5.2 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix similar meta query

## auto-av-images-parser: 0.5.1 (Mon, 23 Aug 2021 18:59:00 +0300)

 * bump
 * fix compare meta
 * fix ocr meta options set
 * raise when yql queries fail
 * add scheduler job for generate ocr
 * fix generate ocr content yql query

## auto-av-images-parser: 0.5.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-185: license plates from ocr

## auto-av-images-parser: 0.4.4 (Mon, 23 Aug 2021 18:59:00 +0300)

 * update pet res id
 * wait for all blocks in nirvana

## auto-av-images-parser: 0.4.3 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix retrying in generate meta

## auto-av-images-parser: 0.4.2 (Mon, 23 Aug 2021 18:59:00 +0300)

 * bump

## auto-av-images-parser: 0.4.1 (Mon, 23 Aug 2021 18:59:00 +0300)

 * don't pick images with 100% similarity
 * fix compare meta query

## auto-av-images-parser: 0.4.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-186: optimize images load
 * clear prometheus directory on start

## auto-av-images-parser: 0.3.4 (Mon, 23 Aug 2021 18:59:00 +0300)

 * catch ClientResponseError in generate pet meta
 * lock message to debug
 * fix dt check in process meta, generate meta
 * fix max day check in fill request queue

## auto-av-images-parser: 0.3.3 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fill request queue joining with log to not load images twice

## auto-av-images-parser: 0.3.2 (Mon, 23 Aug 2021 18:59:00 +0300)

 * change lsh_vectors path

## auto-av-images-parser: 0.3.1 (Mon, 23 Aug 2021 18:59:00 +0300)

 * check compare meta success

## auto-av-images-parser: 0.3.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-183: compare meta task

## auto-av-images-parser: 0.2.21 (Mon, 23 Aug 2021 18:59:00 +0300)

 * catch rpc exception in generate meta

## auto-av-images-parser: 0.2.20 (Mon, 23 Aug 2021 18:59:00 +0300)

 * optimise process meta and generate meta to not generate duplicates

## auto-av-images-parser: 0.2.19 (Mon, 23 Aug 2021 18:59:00 +0300)

 * disable max_inactive_connection_lifetime
 * clear prometheus on exit, gauge in liveall mode

## auto-av-images-parser: 0.2.18 (Mon, 23 Aug 2021 18:59:00 +0300)

 * new pet id

## auto-av-images-parser: 0.2.17 (Mon, 23 Aug 2021 18:59:00 +0300)

 * return gauge

## auto-av-images-parser: 0.2.16 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix queue size metric type

## auto-av-images-parser: 0.2.15 (Mon, 23 Aug 2021 18:59:00 +0300)

 * always use new session for zora requests

## auto-av-images-parser: 0.2.14 (Mon, 23 Aug 2021 18:59:00 +0300)

 * don't remove content path after generate meta

## auto-av-images-parser: 0.2.13 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix fill request queue

## auto-av-images-parser: 0.2.12 (Mon, 23 Aug 2021 18:59:00 +0300)

 * write content yt without lock with redis queue
 * increase zora priority on request fail

## auto-av-images-parser: 0.2.11 (Mon, 23 Aug 2021 18:59:00 +0300)

 * increase load images running tasks max size
 * write content to yt without lock to increase speed (attempt #1)

## auto-av-images-parser: 0.2.10 (Mon, 23 Aug 2021 18:59:00 +0300)

 * add images queue size to metrics

## auto-av-images-parser: 0.2.9 (Mon, 23 Aug 2021 18:59:00 +0300)

 * use redis queue for load images in an attempt to increase speed

## auto-av-images-parser: 0.2.8 (Mon, 23 Aug 2021 18:59:00 +0300)

 * optimise images loading to not run too many tasks at the same time
 * additional logging for redic lock to profile
 * separate db ids from avito ids for better sorting
 * increase lock job ttl

## auto-av-images-parser: 0.2.7 (Mon, 23 Aug 2021 18:59:00 +0300)

 * don't lock some jobs

## auto-av-images-parser: 0.2.6 (Mon, 23 Aug 2021 18:59:00 +0300)

 * increase job lock timeout

## auto-av-images-parser: 0.2.5 (Mon, 23 Aug 2021 18:59:00 +0300)

 * pass 100k urls to load images

## auto-av-images-parser: 0.2.4 (Mon, 23 Aug 2021 18:59:00 +0300)

 * run scheduler tasks until there is nothing to process
 * use msk timezone to comply with other services
 * fix redlock

## auto-av-images-parser: 0.2.3 (Mon, 23 Aug 2021 18:59:00 +0300)

 * create session for every zora request

## auto-av-images-parser: 0.2.2 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix warning log level name for infra

## auto-av-images-parser: 0.2.1 (Mon, 23 Aug 2021 18:59:00 +0300)

 * create table later in write_to_yt

## auto-av-images-parser: 0.2.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * add nirvana meta process/post-process
 * various deploy fixes
 * fix drop cdn
 * add additional job metrics
 * insert ignore queries

## auto-av-images-parser: 0.1.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * initial release
