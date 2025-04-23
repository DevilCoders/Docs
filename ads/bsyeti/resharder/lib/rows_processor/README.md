## Logs processor

Library converts original raw log record into a binary event message and split messages by profile_id into shards. 
### Parsers
Currently is supported the following formats:
* JSON (which hierarchical structure)
* TSKV (tab separated key value) 
* TSV (tab separated values)

There are 2 kinds of fields: common fields and message fields (which are specified in protobuf schema).
The common fields are:

* TimeStamp - record timestamp
* StandVersion - the version of stand from where the log record
* ProfileID - big profile id 
* UniqID - Unique user identifier
* Puid - Yandex Passport identifier
* Gaid - Google device identifier 
* Idfa - Apple device identifier
* Duid - Domain specific user identifier 
* CryptaID - crypt user identifier (version 1.0)
* CryptaID2 - crypt user id identifier (version 2)

Parsing rules for common fields and message fields:
* if there is no mapping in config for common field - it will be skipped even will be met in log
* it there is no mapping for message field, the field name from protobuf will be used.

### Sharding
Library split records by ProfileID into shards.
if there is no ProfileID in a log record, ProfileID can be resolved from other
user identifiers.
In case if there is no ProfileID and no user identifiers a log record will be skipped. 
