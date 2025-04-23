## gpstiles_realtime lb_client configuration
### Proto schema for LogBroker read access settings
Consumer config is provided in **text protobuf** format.
For basic consumer configuration see description at https://wiki.yandex-team.ru/kikimr/persqueue/clib/#nastrojjki and TSettings comments in `kikimr/persqueue/sdk/deprecated/cpp/v1/persqueue.h`.

Settings which must be checked and set:
 - `Topic`, `LogType`
   Terminology brainbreaks. `Topic` here is `Ident` in LogBroker's terminology.
   *For example:* topicId = *"maps_analyzer_tracks\-\-analyzer-dispatcher-signals-log"* => `Topic`=*"maps_analyzer_tracks"*, `LogType`=*"analyzer-dispatcher-signals-log"*.
 - `ClientId`: identifier of consumer as configured in LogBroker ACL.
 - `ServerHostname`: for example: *sas.logbroker.yandex.net*
 - `UseMirroredPartitions`: read/do not read mirrored topics for specified topicId:
   - `False`: read only original topic (data which are written in local DC)
   - `True`: read all data (*'full flow'*): original topic in local DC + all topics mirrored from other DCs to local.
   **Note**: see `MaxPartitions` setting warning.
 - `Threads`: persqueue lib thread pool size (max number of reading threads).
   **Note**: unlike `MaxPartitions`, threads count must not necessarily be equal to read partitions count. It should be enough to read all data with satisfying speed. 
 - `EntityId`: a string which uniquely identifies single consumer within all consumers which share the same `ClientId`. If empty string is passed then consumer hostname is used.
   **Warning**: must not contain **"\-\-"** substring. Breaks /pull queries.
 - `MaxPartitions`: max number of topic's partitions which can be locked concurrently.
   **Warning**: this number must be enough to lock at once **all** requested partitions corresponding to specified topicId:
   - when used with `UseMirroredPartitions =`**`False`**, all partitions of original topic in local DC must be count.
   - when used with `UseMirroredPartitions =`**`True`**, all partitions in all DC's - both original and mirrored - of specified topic must be count.
   **Note**: topic write confuguration (DCs, original/mirrored topics) can be checked in LogBroker web interface: https://lb.yandex-team.ru/main/topic/{{topicId}}/advanced
 - `BatchSize`: max number of messages to return in one read query.
   **Note**: one message may contain more than one object. 
 - `CommitTimeLagSec`: when a message is read from LogBroker it will be commited only after this duration (in seconds) has passed.
 - `LagPolicy`: specifies how to treat existing read lag for every partition when consumer starts:
     - `ignore`: read all data from last commited offset.
     - `skip_outdated`: do not read data which is older than specified `CommitTimeLag` (lb_client2: `SkipOutdatedTimeLagSec`). For every partition the required offset will be found and reading will start from these offsets.
     - `skip_all`: read only fresh data which is written after consumer has started.
