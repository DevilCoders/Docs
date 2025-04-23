# Remote Blob Storage Server (RS)

# Unistat signals

itype=remotestorage

FIXME Префикс `basesearch`, `self`, `remote_blob_storage` не несёт смысла.

## connections
* `basesearch_daemon_accepted_conns`
* `basesearch_daemon_conn_cache_size`

## requests
* `basesearch_daemon_requests`
* `basesearch_daemon_5xx_errors`
* `basesearch_daemon_service_unavailable_errors` 503 not enough resources right now
* `remote_blob_storage_chunk_not_loaded` file is abcent
* `remote_blob_storage_mapping_failed` wrong file id or offset beyound eof
* `remote_blob_storage_size_limit_violation`

## reads (each request contains one or more reads)
* `remote_blob_storage_reads`
* `remote_blob_storage_bytes`
* `remote_blob_storage_recovery_reads`
* `remote_blob_storage_recovery_bytes`
* `remote_blob_storage_hedged_reads`
* `remote_blob_storage_hedged_bytes`
* `remote_blob_storage_repeated_reads`
* `remote_blob_storage_repeated_bytes`
* `remote_blob_storage_request_total_size`

## timings
* `self_request_time_mcs` from end reading request (FIXME) till beging writing response
* `self_succeeded_request_time_mcs`
* `self_failed_request_time_mcs`
* `self_total_request_time_mcs` .. till end of writing response

## queue/pipeline
* `basesearch_daemon_user_inflight`
* `basesearch_daemon_disk_inflight`
* `remote_blob_storage_response_buffers`
