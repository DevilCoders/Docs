# gpstiles_realtime lb_client library
LogBroker consumer library, adapter over `kikimr/persqueue/sdk/deprecated/cpp/v2/deprecated` LogBroker C++ API.
Facilities provided:
 - **objects** vs. **messages**: interface consists of *template classes* which allow library client to operate in domain objects instead of text messages.
 - **delayed commit** semantics: for every partition read its offset will be hard-commited to LogBroker with specified *time lag*. It allows all data which is not older than specified duration to be read again from LogBroker after client restarts.
## Terminology
LogBroker data read by consumer is identified with `Ident--LogType` (topic id).
Data for specified topic id can be written in several topics in several DCs. There are original and mirrored topics. Original topic consists of data which is written locally in the same DC. Mirrored topics consist of data written to LogBroker in other DCs and replicated to current DC.
Every topic is also divided in several parts called partitions. Read sessions are created per partition, not per topic. It means that different partitions of the same topic can be read concurrently in different threads of one consumer.
Reading client - consumer - is identified with `ClientId` which is configured in LogBroker ACL.
For every client, its current reading position (offset) within partition is saved (committed) in LogBroker metadata. Offset identifies message from which to read next (can be interpreted as index of first unread message in partition).
Commit can be **hard** - saved at LogBroker metadata - or **soft** - saved only within current read session.
When read session for a partition starts, there are two values passed to reader: last committed offset (offset) and lag size (lag) - total count of messages unread since last commit.
## How it works
LagPolicy parameter passed through config has three possible values: **skip_all** - client starts reading from the current moment (offset + lag), all previous messages (even unread) are skipped, **ignore** - client starts from the committed offset in partititon (offset), **skip_outdated** - client skips messages older than commitTimeLag.
For LagPolicies "ignore" and "skip_outdated" complete reading of all accumulated data (offset + lag at start moment) is marked - use loaded() function if you need to check it.
## How to use
### Provide LogBroker read access config
See readme in `proto` directory where config schema resides.
### Specify parser, time access function and collector for objects
**`include/callbacks.h`**
You must provide function objects (callbacks):
 - converting message to vector of objects:
```c++
	template <class Object>
	using Parser = std::function< std::vector<Object>(const char*, size_t) >;
```
 - accepting read and parsed objects for actual usage:
```c++
	template <class Object>
	using Collector = std::function< void(std::vector<Object>&&) >;
```
 - extracting time from single object:
```c++
	template <class Object>
	using TimeGetter = std::function< TimePoint(const Object&) >;
```
which are united in `ObjectCallbacks` structure to be passed to client instance.
### Start client
**`include/client.h`**
Construct client instance passing parsed config and object callbacks:
```c++
	LBClient(
        const cfg::TConfig& config,
        const ObjectCallbacks<Object>& objectCallbacks)
```
and call `start()` method.
**Ensure** that client's lifetime lies entirely within lifetimes of objects providing parsing and collecting.
## Limitations
 - *Honest* object times are used, so every message must be parsed to determine its avg/max time.
 - Does not support specifying a subset of partitions to be read.
 - [as for 14.05.2018] Use of `TSettings::EFormat::FORMAT_RAW` is hardcoded. Client can only be used for gzipped topics.
## Known issues
 - Two clients reading **the same topics concurrently with same client id** will block each other. All partitions will be divided between two instances in arbitrary way which is easily seen in log messages (log level >= "info"): there will be "read offset"/"commit offset" reports in log only foe a subset of partitions.
 - `MaxPartitions` not enough for actual partitions count. There will be persistent read lag present for some partitions which can be seen via LogBroker web interface (read metrics for specified client id).
 -  "\-\-" in `EntityId` string will result in 100% 400 HTTP Bad Request for all /pull queries. No data will be read at all. Hostnames (which are used as default `EntityId`) containing "\-\-" may be generated when deploying in RTC via GenCfg + Nanny. In this case you should specify some valid `EntityId` yourself. As you can not run more than one instance in one DC (as you read all partitions for specified topics), DC's ID (*"sas"*) is usually enough.
## Usage examples
See:
 - maps/wikimap/gpstiles_realtime/tools/db_writer
 - maps/wikimap/gpstiles_realtime/fastcgi
