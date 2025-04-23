# search/tools/findurl/proto

## Services
### findurl.Findurl
#### postTask([findurl.PostTaskRequest](#message-findurlposttaskrequest-source)) → [findurl.PostTaskResponse](#message-findurlposttaskresponse-source)

#### unistat([google.protobuf.Empty](#message-googleprotobufempty-source)) → [h.unistat.UnistatData](#message-hunistatunistatdata-source)



## Data
### enum findurl.Batch.Status <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/tools/findurl/proto/structures/model.proto)</sup>
- _0_ - **CREATED** _default_

### enum findurl.Task.Status <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/tools/findurl/proto/structures/model.proto)</sup>
- _0_ - **CREATED** _default_
- _1_ - **DOC_ID_RECEIVING**
- _2_ - **DOC_ID_RECEIVED**
- _3_ - **SERP_RECEIVING**
- _4_ - **SERP_RECEIVED**
- _5_ - **STATUS_RECEIVING**
- _6_ - **STATUS_RECEIVED**
- _7_ - **QWE**

### message findurl.Batch <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/tools/findurl/proto/structures/model.proto)</sup>
- **basetype** _string_

- **cgi** _string_

- **doc_id** _string_

- **id** _int64_

- **position** _int64_

- **qloss_status** _string_

- **query** _string_

- **region** _string_

- **relev** _string_

- **shardname** _string_

- **url** _string_


### message findurl.DocIdReceivingTask <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/tools/findurl/proto/structures/model.proto)</sup>
- **batch_id** _int64_


### message findurl.PostTaskRequest <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/tools/findurl/proto/structures/message.proto)</sup>
- **batches** _message[]_ [findurl.Batch](#message-findurlbatch-source)

- **comment** _string_

- **upper_host** _string_


### message findurl.PostTaskResponse <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/tools/findurl/proto/structures/message.proto)</sup>
- **id** _int64_


### message findurl.Task <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/tools/findurl/proto/structures/model.proto)</sup>
- **author** _string_

- **batches** _message[]_ [findurl.Batch](#message-findurlbatch-source)

- **comment** _string_

- **created** _int64_

- **doc_id_receiving_tasks** _message[]_ [findurl.DocIdReceivingTask](#message-findurldocidreceivingtask-source)

- **id** _int64_

- **meta_rearrs** _string[]_

- **status** _enum_ [findurl.Task.Status](#enum-findurltaskstatus-source)

- **upper_host** _string_
