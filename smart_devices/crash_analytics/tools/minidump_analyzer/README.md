# Minidump analyzer

Analyzes [yql_minidump](https://a.yandex-team.ru/arc/trunk/arcadia/yandex_io/tools/yql_minidump) output

## Usage

Let's suppose `yql_minidump` saved its results to `~/minidumps`. Then you can run `minidump_analyzer` as:

```sh
ya m && ./minidump_analyzer ~/minidumps ~/minidumps_analyzed
```

Result of analysis will be saved to `~/minidumps_analyzed` .

## Output explained

You can find an example of the output [here](https://proxy.sandbox.yandex-team.ru/1708510640).

All minidumps are divided into groups by their stacktraces. Each folder in the output contains minidumps of one group. 

Analysis summary can be found in the [report.txt](https://proxy.sandbox.yandex-team.ru/1708510640/report.txt?force_text_mode=1) at the root of the output folder. Inside the report each line indicates the last meaningful line of the stacktrace and its group size, that is, the number of minidumps with stacktraces ending with this line.

For instance:

```
maind!quasar::YandexRadioPlayer::handleBufferingStart() [YandexRadioPlayer.cc : 444 + 0x0] : 42
```

This line means analyzer has found 42 minidumps with stacktraces ending with `YandexRadioPlayer::handleBufferingStart()`. You can look at these minidumps in the folder named [`maind!quasar::YandexRadioPlayer::handleBufferingStart`](https://proxy.sandbox.yandex-team.ru/1708510640/maind!quasar::YandexRadioPlayer::handleBufferingStart).
