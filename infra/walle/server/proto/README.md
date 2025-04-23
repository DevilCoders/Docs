via https://clubs.at.yandex-team.ru/arcadia/24169

16.03.2021
Tried to check syntax with prototool:
```
[ arcadia ] $ ~/go/bin/prototool lint infra/walle/server/proto/walle/scenario/data_storage/v1/scenario_data_storage.proto 
infra/walle/server/proto/walle/scenario/data_storage/v1/scenario_data_storage.proto:1:1:File option "go_package" is required.
infra/walle/server/proto/walle/scenario/data_storage/v1/scenario_data_storage.proto:1:1:File option "java_multiple_files" is required.
infra/walle/server/proto/walle/scenario/data_storage/v1/scenario_data_storage.proto:1:1:File option "java_outer_classname" is required.
infra/walle/server/proto/walle/scenario/data_storage/v1/scenario_data_storage.proto:1:1:File option "java_package" is required.
infra/walle/server/proto/walle/scenario/data_storage/v1/scenario_data_storage.proto:3:1:The name "walle.scenario.data_storage.v1" contains the outlawed name "data". Data is a decorator and all types on Protobuf are data, consider merging this information into a higher-level type, or if you must have such a type, Use "Info" instead..
infra/walle/server/proto/walle/scenario/data_storage/v1/scenario_data_storage.proto:3:1:Packages should only contain characters in the range a-z0-9 and periods but was "walle.scenario.data_storage.v1".
infra/walle/server/proto/walle/scenario/data_storage/v1/scenario_data_storage.proto:6:1:The name "ScenarioDataStorage" contains the outlawed name "data". Data is a decorator and all types on Protobuf are data, consider merging this information into a higher-level type, or if you must have such a type, Use "Info" instead..
infra/walle/server/proto/walle/scenario/data_storage/v1/scenario_data_storage.proto:7:5:The name "data_storage" contains the outlawed name "data". Data is a decorator and all types on Protobuf are data, consider merging this information into a higher-level type, or if you must have such a type, Use "Info" instead..
infra/walle/server/proto/walle/scenario/data_storage/v1/scenario_data_storage.proto:8:9:The name "itdc_maintenance_data_storage" contains the outlawed name "data". Data is a decorator and all types on Protobuf are data, consider merging this information into a higher-level type, or if you must have such a type, Use "Info" instead..
infra/walle/server/proto/walle/scenario/data_storage/v1/scenario_data_storage.proto:12:1:The name "ItdcMaintenanceDataStorage" contains the outlawed name "data". Data is a decorator and all types on Protobuf are data, consider merging this information into a higher-level type, or if you must have such a type, Use "Info" instead..

[ proto ] $ pwd
/home/squirrel/arcadia/infra/walle/server/proto

[ proto ] $ ~/go/bin/prototool version
Version:                 1.10.0
Default protoc version:  3.11.0
Go version:              go1.15.8
OS/Arch:                 linux/amd64
```

