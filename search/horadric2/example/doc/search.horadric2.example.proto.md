# search/horadric2/example/proto

## Services
### example.services.Randomizer
#### getAuthProtectedRandomInt([google.protobuf.Empty](#message-googleprotobufempty-source)) → [example.RandomResponse](#message-examplerandomresponse-source)

#### getRandomInt([google.protobuf.Empty](#message-googleprotobufempty-source)) → [example.RandomResponse](#message-examplerandomresponse-source)

#### getRandomNestedMessage([google.protobuf.Empty](#message-googleprotobufempty-source)) → [example.RandomResponse](#message-examplerandomresponse-source)

#### getRandomNestedMessages([google.protobuf.Empty](#message-googleprotobufempty-source)) → [example.RandomResponse](#message-examplerandomresponse-source)

#### getRandomRepeatedInt([google.protobuf.Empty](#message-googleprotobufempty-source)) → [example.RandomResponse](#message-examplerandomresponse-source)

#### testProxy([example.RandomResponse](#message-examplerandomresponse-source)) → [example.RandomResponse](#message-examplerandomresponse-source)

#### unistat([google.protobuf.Empty](#message-googleprotobufempty-source)) → [h.unistat.UnistatData](#message-hunistatunistatdata-source)


### zephyr.ConfigGenerator
#### buildConfig([zephyr.ProjectFilter](#message-zephyrprojectfilter-source)) → [zephyr.ProjectConfig](#message-zephyrprojectconfig-source)

#### getConfig([zephyr.ProjectConfigFilter](#message-zephyrprojectconfigfilter-source)) → [zephyr.ProjectConfig](#message-zephyrprojectconfig-source)

#### setConfigStatus([zephyr.SetConfigStatusRequest](#message-zephyrsetconfigstatusrequest-source)) → [zephyr.ProjectConfig.StatusChange](#message-zephyrprojectconfigstatuschange-source)


### zephyr.ServiceDiscovery
#### getProject([zephyr.ProjectFilter](#message-zephyrprojectfilter-source)) → [zephyr.Project](#message-zephyrproject-source)

#### listInstances([zephyr.InstanceFilter](#message-zephyrinstancefilter-source)) → [zephyr.MappedInstanceList](#message-zephyrmappedinstancelist-source)

#### listProjects([zephyr.ProjectBatchFilter](#message-zephyrprojectbatchfilter-source)) → [zephyr.ProjectList](#message-zephyrprojectlist-source)

#### reportHealth([zephyr.HealthReport](#message-zephyrhealthreport-source)) → [google.protobuf.Empty](#message-googleprotobufempty-source)



## Data
### enum example.EnumAlpha <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/pyitest.proto)</sup>
- _0_ - **R_UNDEFINED** _default_
- _1_ - **R_LOL**
- _2_ - **R_WTF**

### enum example.RandomResponse.NestedEnum <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/random.proto)</sup>
- _0_ - **LOL** _default_
- _1_ - **WTF**

### enum example.Status <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/random.proto)</sup>
- _0_ - **OK** _default_
- _1_ - **OPERATOR_IS_NOT_ADMIN**
- _2_ - **TAG_IS_MISSING**
- _3_ - **TAG_ALREADY_EXISTS**

### enum example.TestAlpha.NestedEnumAlpha <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/pyitest.proto)</sup>
- _0_ - **N_UNDEFINED** _default_
- _1_ - **N_LOL**
- _2_ - **N_WTF**

### enum example.TestEnum <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/random.proto)</sup>
- _0_ - **UNKNOWN** _default_
- _1_ - **LOL**

### enum zephyr.Geo <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- _0_ - **UNKNOWN** _default_
- _1_ - **SAS**
- _2_ - **MAN**
- _3_ - **VLA**

### enum zephyr.ProjectConfig.Status <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- _0_ - **PREPARED** _default_
- _1_ - **ACTIVE**

### message example.ChangeTagResponse <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/random.proto)</sup>
- **operation_status** _enum_ [example.Status](#enum-examplestatus-source)

- **tag_item** _message_ [example.TagItem](#message-exampletagitem-source)


### message example.RRandomResponse <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/random.proto)</sup>
- **rrr** _message[]_ [example.RandomResponse](#message-examplerandomresponse-source)


### message example.RandomResponse <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/random.proto)</sup>
- **nested_enum** _enum_ [example.RandomResponse.NestedEnum](#enum-examplerandomresponsenestedenum-source)

- **nested_message** _message_ [example.RandomResponse.NestedMessage](#message-examplerandomresponsenestedmessage-source)

- **random_enum** _enum_ [example.TestEnum](#enum-exampletestenum-source)

- **random_int** _uint64_

- **repeated_enum** _enum[]_ [example.TestEnum](#enum-exampletestenum-source)

- **repeated_int** _uint64[]_

- **repeated_nested_enum** _enum[]_ [example.RandomResponse.NestedEnum](#enum-examplerandomresponsenestedenum-source)

- **repeated_nested_message** _message[]_ [example.RandomResponse.NestedMessage](#message-examplerandomresponsenestedmessage-source)

- **str_message_map** _map_ string → [example.RandomResponse.NestedMessage](#message-examplerandomresponsenestedmessage-source)

- **str_u64_map** _map_ string → uint64

- **u64_enum_map** _map_ uint64 → [example.RandomResponse.NestedEnum](#enum-examplerandomresponsenestedenum-source)


### message example.RandomResponse.NestedMessage <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/random.proto)</sup>
- **lol** _bool_


### message example.TagItem <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/random.proto)</sup>
- **id** _uint64_

- **name** _string_


### message example.TestAlpha <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/pyitest.proto)</sup>
- **boolean** _bool_

- **string** _string_

- **ui64** _uint64_


### message example.TestAlpha.NestedMessageAlpha <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/pyitest.proto)</sup>
- **bar** _string_

- **baz** _message_ [example.TestAlpha](#message-exampletestalpha-source)

- **foo** _enum_ [example.TestAlpha.NestedEnumAlpha](#enum-exampletestalphanestedenumalpha-source)


### message example.TestAlpha.NestedMessageAlpha.NestedNestedMessageAlpha <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/pyitest.proto)</sup>
- **bar** _string_

- **baz** _message_ [example.TestAlpha](#message-exampletestalpha-source)

- **foo** _enum_ [example.TestAlpha.NestedEnumAlpha](#enum-exampletestalphanestedenumalpha-source)

- **lol** _message_ [example.TestAlpha.NestedMessageAlpha](#message-exampletestalphanestedmessagealpha-source)


### message example.TestBravo <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/pyitest.proto)</sup>
- **alpha_enums** _enum[]_ [example.TestAlpha.NestedEnumAlpha](#enum-exampletestalphanestedenumalpha-source)

- **alphas** _message[]_ [example.TestAlpha](#message-exampletestalpha-source)

- **rep_str** _string[]_


### message zephyr.HealthReport <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **access_key** _string_

- **instance** _message_ [zephyr.Instance](#message-zephyrinstance-source)

- **time** _float_


### message zephyr.Instance <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **fqdn** _string_

- **geo** _enum_ [zephyr.Geo](#enum-zephyrgeo-source)

- **methods** _message[]_ [zephyr.Method](#message-zephyrmethod-source)

- **port** _uint32_

- **ssl** _string[]_


### message zephyr.InstanceFilter <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **method** _string_

- **service** _string_


### message zephyr.MappedInstance <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **instance** _message_ [zephyr.Instance](#message-zephyrinstance-source)

- **project** _string_

- **stage** _string_


### message zephyr.MappedInstanceList <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **objects** _message[]_ [zephyr.MappedInstance](#message-zephyrmappedinstance-source)


### message zephyr.Method <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **input** _string_

- **name** _string_

- **output** _string_

- **retries** _uint32_

- **service** _string_

- **timeout** _float_

- **version** _float_


### message zephyr.Project <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **name** _string_

- **owners** _uint64[]_

- **stages** _message[]_ [zephyr.Stage](#message-zephyrstage-source)


### message zephyr.ProjectBatchFilter <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **names** _string[]_


### message zephyr.ProjectConfig <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **built_at** _float_

- **history** _message_ [zephyr.ProjectConfig.History](#message-zephyrprojectconfighistory-source)

- **id** _string_

- **project** _message_ [zephyr.Project](#message-zephyrproject-source)

- **status** _enum_ [zephyr.ProjectConfig.Status](#enum-zephyrprojectconfigstatus-source)


### message zephyr.ProjectConfig.History <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **objects** _message[]_ [zephyr.ProjectConfig.StatusChange](#message-zephyrprojectconfigstatuschange-source)


### message zephyr.ProjectConfig.StatusChange <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **reqid** _string_

- **source** _enum_ [zephyr.ProjectConfig.Status](#enum-zephyrprojectconfigstatus-source)

- **target** _enum_ [zephyr.ProjectConfig.Status](#enum-zephyrprojectconfigstatus-source)

- **time** _float_


### message zephyr.ProjectConfigFilter <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **id** _string_


### message zephyr.ProjectFilter <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **name** _string_


### message zephyr.ProjectList <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **objects** _message[]_ [zephyr.Project](#message-zephyrproject-source)


### message zephyr.SetConfigStatusRequest <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **id** _string_

- **target** _enum_ [zephyr.ProjectConfig.Status](#enum-zephyrprojectconfigstatus-source)


### message zephyr.Stage <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/proto/structures/zephyr.proto)</sup>
- **accessKey** _string_

- **hosts** _string[]_

- **instances** _message[]_ [zephyr.Instance](#message-zephyrinstance-source)

- **name** _string_

- **ssl** _string[]_
