# Thread Telemetry Tool

## Tp stack
Collects stacks from tp task

### Usage
Find running task, e.g [Serp Update](https://tp.yandex-team.ru/tp/metrics-join/3a69a192-dc03-4a86-8773-08e81223dc7c).

Collect stacks
```bash
./ttt metrics-join 3a69a192-dc03-4a86-8773-08e81223dc7c > stacks
```

Then build [FlameGraph](https://github.com/brendangregg/FlameGraph):

```bash
./stackcollapse-java-exceptions.pl < stacks > fold
./flamegraph.pl fold > flamegraph.svg
```

### Collect compare stacks
Run on couple of nodes
```bash
./ttt stack irpmr63hqwkxf76m.sas.yp-c.yandex.net 'BatchJoinedSerpCalculatorImpl.processInner' >> stacks
```

Join and filter stacks
```bash
cat stacks | grep -v locked | grep -v reflect | grep -v Lambda > stacks_filtered
```

Build flamegraph
```bash
./stackcollapse-java-exceptions.pl < stacks_filtered > fold
./flamegraph.pl fold > flamegraph.svg
```

### Collect stacks for time window

```bash
ya make; ./ttt stack_collect "21-11-16 2:10" "21-11-16 22:10" dump_directory jw7v3m7o45cmtoho.sas.yp-c.yandex.net ag34dud4cp6pbqiw.vla.yp-c.yandex.net cwa5qu25szfcnr7e.man.yp-c.yandex.net --every 100
```
