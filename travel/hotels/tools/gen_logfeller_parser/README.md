# Logfeller Parser Config Generator

## How To

- Add your proto module into `ya.make` dependencies of this generator module
- Import the needed proto components into `main.cpp`:
```
#include "<$A/proto/file/path>.pb.h"
```
- In the same file, for every log type add a separate log record structure conversion config:
```
    logFactory.emplace("<generated_log_alias>", TLogDescription{
                               THolder(new NTravelProto::<your_package>::<your_proto_log_entity>()),
                               "<logfeller_parser_config_name>.json",
                               false
                           });
```
- Rebuild the generator:
```
ya make
```
- Run it to get the needed parser config file:
```
gen_logfeller_parser % ./gen_logfeller_parser -l <generated_log_alias>
New config is written to /path/to/arcadia/logfeller/configs/parsers/<logfeller_parser_config_name>.json , don't forget to commit it!
```
- If the command above fails with the 'No such file or directory' error, try to check the configs dir out first:
```
ya make --checkout -j0 arcadia/logfeller/configs/parsers/
```
- Commit the generated config
