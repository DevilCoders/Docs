# infra/callisto/protos/multibeta

## Data
### enum infra.callisto.Component.Status <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/slot_state.proto)</sup>
- _0_ - **UNKNOWN** _default_
- _1_ - **READY**
- _2_ - **WAIT_FOR_QUORUM**

### enum infra.callisto.Response.Error <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/slot_state.proto)</sup>
- _0_ - **NO_ERROR** _default_
- _1_ - **UNKNOWN_SLOT**
- _2_ - **UNKNOWN_REVISION**

### enum infra.callisto.Response.Status <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/slot_state.proto)</sup>
- _0_ - **UNKNOWN** _default_
- _1_ - **READY**
- _2_ - **WAIT_FOR_QUORUM**

### message infra.callisto.Component <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/slot_state.proto)</sup>
- **description** _string_

- **diagnostics** _message_ [infra.callisto.Component.Diagnostics](#message-infracallistocomponentdiagnostics-source)

- **instances** _message_ [infra.callisto.Component.Progress](#message-infracallistocomponentprogress-source)

- **shards** _message_ [infra.callisto.Component.Progress](#message-infracallistocomponentprogress-source)

- **status** _enum_ [infra.callisto.Component.Status](#enum-infracallistocomponentstatus-source)


### message infra.callisto.Component.Diagnostics <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/slot_state.proto)</sup>
- **oom_kills** _message_ [infra.callisto.Component.Diagnostics.OOM](#message-infracallistocomponentdiagnosticsoom-source)

- **respawns** _message_ [infra.callisto.Component.Diagnostics.Respawns](#message-infracallistocomponentdiagnosticsrespawns-source)


### message infra.callisto.Component.Diagnostics.OOM <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/slot_state.proto)</sup>
- **median** _int64_

- **total** _int64_


### message infra.callisto.Component.Diagnostics.Respawns <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/slot_state.proto)</sup>
- **median** _int64_

- **total** _int64_


### message infra.callisto.Component.Progress <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/slot_state.proto)</sup>
- **observed_count** _int64_

- **required_count** _int64_


### message infra.callisto.ImgFreshBeta <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/quick.proto)</sup>
- **index_generation** _string_

- **mmeta** _message_ [infra.callisto.Mmetasearch](#message-infracallistommetasearch-source)

- **quick** _message_ [infra.callisto.RtyBasesearch](#message-infracallistortybasesearch-source)

- **ultra** _message_ [infra.callisto.RtyBasesearch](#message-infracallistortybasesearch-source)


### message infra.callisto.InstanceInfo <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/slot_state.proto)</sup>
- **hostname** _string_

- **port** _uint64_


### message infra.callisto.Mmetasearch <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/quick.proto)</sup>
- **config** _message_ [infra.callisto.Resource](#message-infracallistoresource-source)

- **executable** _message_ [infra.callisto.Resource](#message-infracallistoresource-source)

- **models** _message_ [infra.callisto.Resource](#message-infracallistoresource-source)

- **pure_index** _message_ [infra.callisto.Resource](#message-infracallistoresource-source)

- **rearrange_data** _message_ [infra.callisto.Resource](#message-infracallistoresource-source)

- **rearrange_index** _message_ [infra.callisto.Resource](#message-infracallistoresource-source)


### message infra.callisto.Request <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/slot_state.proto)</sup>
- **revision** _uint64_

- **slot_id** _string_


### message infra.callisto.Resource <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/quick.proto)</sup>
- **extract** _bool_

- **path** _string_

- **url** _string_


### message infra.callisto.Response <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/slot_state.proto)</sup>
- **components** _message[]_ [infra.callisto.Component](#message-infracallistocomponent-source)

- **error** _enum_ [infra.callisto.Response.Error](#enum-infracallistoresponseerror-source)

- **instances** _message[]_ [infra.callisto.InstanceInfo](#message-infracallistoinstanceinfo-source)

- **status** _enum_ [infra.callisto.Response.Status](#enum-infracallistoresponsestatus-source)


### message infra.callisto.RtyBasesearch <sup>[source](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/protos/multibeta/quick.proto)</sup>
- **config** _message_ [infra.callisto.Resource](#message-infracallistoresource-source)

- **executable** _message_ [infra.callisto.Resource](#message-infracallistoresource-source)

- **models** _message_ [infra.callisto.Resource](#message-infracallistoresource-source)

- **static_models** _message_ [infra.callisto.Resource](#message-infracallistoresource-source)
