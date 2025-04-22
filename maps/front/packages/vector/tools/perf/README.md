# Performance test tool

## Usage
The tool runs `Vector` with specified camera scenario and collects stats from these runs. Stats are then aggregated and
shown on chart.

**Scenario** is a sequence of actions for camera.

**Test** consists of scenario repeated specified amount of times in one of the envs/stands. For now supported stands are
`dev` and `jsapi`, probably there will be `maps` stand as well.

### Run test
```sh
# Builds tool with current version of vector and runs server
make perf
```
When server is started, open `http://localhost:3000` in browser. There you can configure
and run a new test or observe existing stats.

### Observe stats
```sh
# Runs server without building
make perf-start
```
Use this to see collected stats or run already built version.
Be careful when using this option and running tests because it will use old build (if any).

### Stop test
To stop running test go to `http://localhost:3000#stop`.

### Scenarios
Scenarios are defined as functions in the source code of the tool, in `<perf_tool>/scenarios/index.ts`. Scenario's name
is defined with the key of exported object - `allScenarios`.
```ts
interface Scenario {
    (stand: Stand): Promise<any>;
}
interface Stand {
    create(zoom?: number, center?: Vector2): Promise<void>;
    moveTo(x: number, y: number, duration: number): Promise<void>;
    zoomTo(zoom: number, duration: number): Promise<void>;
    waitForAllTiles(): Promise<void>;
}
```
It is convenient to test your scenario with `make perf-dev`.

### Run with headless browser
First, create `<perf_tool>/config.js`, use `<perf_tool>/config.example.json` as a reference.
Then you can run test using command:
```sh
make perf-headless RUNS="<number of runs>" SCENARIO="<scenario name>" STAND="<stand type>" TAG="<test tag>"
#For example
make perf-headless RUNS=20 SCENARIO=moscow STAND=dev TAG=headless_test
```
Stats will be stored in the `<perf_tool>/stats` dir. You can upload them from tool UI to see charts (`make perf-start`,
for example).

### Control over the build
`make perf` and `make perf-headless` compiles current version before each run and stores in the `out` dir. You
can do it manually and skip this stage before the run:
```sh
# Builds tool with current version of vector and stores to `out` (inside the tool dir)
make perf-build
# Runs server so you can see stats or run tests with pre-built version
make perf-start
# Runs headless tests with pre-built version
make perf-headless-run RUNS="<number of runs>" SCENARIO="<scenario name>" STAND="<stand type>" TAG="<test tag>"
```

## Contributing
To run dev server do
```sh
make perf-dev
```
and proceed to `http://localhost:3000`
