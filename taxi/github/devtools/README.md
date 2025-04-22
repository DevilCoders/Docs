# devtools
## Installation
```bash
# Install using apt
sudo apt install taxi-devtools

# Install using pip, Python version >=3.7 is required
cd arcadia/taxi/github/devtools/ && pip3 install -i https://pypi.yandex-team.ru/simple/ .

# Manually build deb package
debuild -b
dpkg -i ../taxi-devtools_XXXX.deb
```

## Configration

Create configuration containing your tokens `~/.taxi-devtools`:

```ini
[default]

# Visit https://github.yandex-team.ru/settings/tokens to receive your
# github token. Do not forget to enable repo checkboxes.
github-token = secret-token

# Visit https://wiki.yandex-team.ru/tracker/api/#avtorizacija to receive
# your startrek token.
startrek-token = secret-token
```

Your can override some values in repo local config file repo.git/.taxi-devtools:

```ini
[default]
# This repo has master as its base branch
base-branch = master
```

To access nanny hosts for nuter:
Get nanny token from http://nanny.yandex-team.ru/ui/#/oauth/
And put it to `~/.nanny_token`

To setup psql connection timeout put it to `~/.nanny_token`, otherwise default 2 seconds will be used:

```ini
[nuter]

pg-connection-timeout = <connection timeout in seconds>
```

## Setup Taxi developer's environment

### Ubuntu
To prepare your Ubuntu for working with Taxi's repositories run
`scripts/setup-ubuntu-env.sh` using Curl:
```bash
bash <(curl -s https://raw.github.yandex-team.ru/taxi/devtools/develop/scripts/setup-ubuntu-env.sh)
```

## Create pull request

```bash
(develop) repo$ git fetch upstream develop
(develop) repo$ git checkout -b feature-branch upstream/develop
(feature-branch) repo$ # hack hack hack
(feature-branch) repo$ git commit
(feature-branch) repo$ git create-pr
...
https://github.yandex-team.ru/taxi/repo/pull/number
```

You can use `team-label` config to mark all your PR by a label of your team.

Example:
```ini
[create-pr]
team-label = product_group_1
```

Note: this label must be existing in a repository otherwise it will be ignored!

## Create schemas pull request

```bash
(feature-branch) repo$ git create-schemas-pr
...
https://github.yandex-team.ru/taxi/schemas/pull/4210
```

## Working with taxi config from command line

In order to work with taxi-config tool you need to add tariff editor token to
your `~/.taxi-devtools`:

```ini
[default]

# Visit https://wiki.yandex-team.ru/taxi/backend/Adminka-bez-koda/#oauth
# to obtain tariff-editor token.
tariff-editor-token = SECRET-TOKEN
```

### Retrieve config value
```bash
# Retrieve production value
$ taxi-config get PASS_AUTH_ROUTER_RULES_2
# Retrieve testing value
$ taxi-config -e testing get PASS_AUTH_ROUTER_RULES_2
```

### Grep config value
```bash
# Grep configs identified by CARGO regex for lavka pattern
$ taxi-config grep lavka CARGO
```

## Experiments3.0 tool

### List experiment3.0/config3.0
```bash
# List experiments3.0
$ taxi-exp3 exp3-list
# List configs3.0
$ taxi-exp3 configs-list
```

### Retrieve experiment3.0/config3.0 value
```bash
$ taxi-exp3 exp3-get advert_on_map
$ taxi-exp3 configs-get banlist
```

### Grep experiment3.0/config3.0 value
```bash
$ taxi-exp3 exp3-grep lavka cargo
$ taxi-exp3 configs-grep lavka cargo
```

## Working with clownductor from command line

### Show packages versions
```bash
# Show 'envoy-exp-alpha' versions in testing
$ clown --env testing versions --package-name envoy-exp-alpha
# Show versions of all packages from all hosts in production
$ clown versions --all
```

## TVM helpers
### Perform request with sshkey ticket

```bash
$ taxi-tvm-curl avatars-mds -v http://avatars-int.mdst.yandex.net:13000/getinfo-grocery-goods/65694/2128a73ee92b4b4c83b80c513f4bf2a1/orig > /dev/null
```

### TVM rules helper

```bash
# List tvm services
$ taxi-tvm services

# List tvm rules
$ taxi-tvm rules [--src zalogin] [--dst antifraud]

# Format tvm rule as json
$ taxi-tvm format-rule -s zalogin -d antifraud
```

## Execute commands at nanny services
**N**anny exec**uter**, like executer but will start faster
```bash
$ nuter ssh taxi_api-proxy_pre_stable
$ nuter ssh taxi_api-proxy_pre_stable -p 2222  # also works
$ nuter ssh taxi_api-proxy_pre_stable tail -f /var/log/yandex/taxi-api-proxy/server.log  # also works
$ nuter hostlist taxi_api-proxy_stable  # will list hosts
$ nuter psql lavka_grocery-cart_testing  # run psql against grocery-cart's database
```

This tools does not have groups registry, but will remember groups
you connect to and propose completion for subsequent requests

Nuter supports `p_exec`, parallel command execution at every pod of group (pay attention prestable is not 
a part of stable in RTC)
```bash
nuter p_exec taxi_api-proxy_pre_stable ls --color  # Will use port 2222 autmatically for RTC services
nuter p_exec --root taxi_api-proxy_tesing ls --color  # Override port 2222
```

Nutter also introduces `logs` and `errors` commands to view logs at services (it tries to guess log location)
```bash
nuter logs taxi_api-proxy_testing 
nuter errors taxi_api-proxy_testing 
nuter logs --level=WARN -F -N -n 60 taxi_api-proxy_testing -o "'meta_type=[^	]*'"
nuter logs --level=WARN -F -n 60 taxi_api-proxy_testing stopwatch '| print_cpp_timings.py'
nuter logs --help  # try it!
```

## Retrieve taxi order

Using `taxi-order-retrieve` tool you can retrieve taxi order document, e.g.:

```bash
$ taxi-order-retrieve 7bb913229736276aa7d3fdd6ae8ad09e
$ taxi-order-retrieve -t order 7bb913229736276aa7d3fdd6ae8ad09e
$ taxi-order-retrieve --pretty 7bb913229736276aa7d3fdd6ae8ad09e
$ taxi-order-retrieve -e production 81308c4c75d71712ab437f90e0c6152b
```

## Retrieve ProcaaS state

More details: https://wiki.yandex-team.ru/taxi/backend/architecture/processing/manualprocaas/#utilitadljaprosmotratekushhegosostojanijataxi-devtools

### Retrieve events

Get all events for specified scope/queue/item.
Will restore events from YT if needed.

API reference: https://a.yandex-team.ru/arc/trunk/arcadia/taxi/uservices/services/processing/docs/yaml/api/api.yaml?rev=r8782491#L167

```bash
$ procaas events taxi orders 4faf9089865fca17bc72386a45b5487f
$ procaas -e testing events taxi orders 4faf9089865fca17bc72386a45b5487f
```

### Retrieve current state

Get current state for specified scope/queue/item.
Will restore events from YT if needed.

API reference: https://a.yandex-team.ru/arc/trunk/arcadia/taxi/uservices/services/processing/docs/yaml/api/api.yaml?rev=r8782491#L215

```bash
$ procaas state taxi orders 4faf9089865fca17bc72386a45b5487f
$ procaas -e testing state taxi orders 4faf9089865fca17bc72386a45b5487f
$ procaas state taxi orders 4faf9089865fca17bc72386a45b5487f --terminal-event d0296e1e8d594b6e820c557683b84836
```

### Retrieve checkpoint

Get checkpoint of the currently running pipeline for specified
scope/queue/item. Checkpoint - stage, `shared_state`, etc. describing
place from which pipeline will continue/restart(in case of failed
stage) execution.

API reference: https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/processing/docs/yaml/api/api.yaml?rev=r8908297#L215

```bash
$ procaas checkpoint taxi orders 40aa61bee8cdc66aacbe9ef3bc2dbec6
$ procaas -e testing checkpoint taxi orders 40aa61bee8cdc66aacbe9ef3bc2dbec6
```

Getting an error:
```json
{
  "error": "No such item or checkpoint ..."
}
```
means that either item with specified `item_id` doesn't exists or
there is no checkpoint for this item: pipeline finished successfully
and there is no point to run execution from.

### Retrieve current state

### Retrieve from external procaas instance

```bash
$ procaas events taxi orders 4faf9089865fca17bc72386a45b5487f --serivce-url processing.taxi.tst.yandex.net
$ procaas state taxi orders 4faf9089865fca17bc72386a45b5487f --serivce-url processing.taxi.tst.yandex.net --tvm-src-id 2013636 --tvm-dst-id 2016733
```

## Candidates
### Run order-satisfy

```bash
$ taxi-order-satisfy -p 34.749494,32.009169 -d 3baf5e9978364461abc7b592794b467f_0eb262402177ed7837e1ad48d570b242 --shift-group=6871
```

## Find cargo claim
Try to match requested_id to segment_id, cargo_order_id, claim_id, waybill_ref, cargo_ref_id or taxi_order_id and show claim information.

Using `cargo-claim-retrieve` tool you can get information about claim in your console

Using `cargo-claim-open` tool you can open claim in your browser
(The main difference between these utils is the way of showing result):
```bash
$ cargo-claim-retrieve 6f4b429175724470bfb0655a463f6421
$ cargo-claim-open 6f4b429175724470bfb0655a463f6421
$ cargo-claim-retrieve -e production 6f4b429175724470bfb0655a463f6421
$ cargo-claim-open -e testing 6f4b429175724470bfb0655a463f6421 ac743c32-3e2b-4de1-8465-0e05de3d7382
```

Using `cargo-claim-open` tool you can get information about claim:

```bash
$ cargo-claim-open 6f4b429175724470bfb0655a463f6421
$ cargo-claim-open -e production 6f4b429175724470bfb0655a463f6421
$ cargo-claim- -e testing 6f4b429175724470bfb0655a463f6421 ac743c32-3e2b-4de1-8465-0e05de3d7382
```
## Teamcity run builds

Using `taxi-teamcity` tool you can run builds.
Setup your `~/.taxi-devtools`:
```ini
[default]

# Visit https://teamcity.taxi.yandex-team.ru/profile.html?item=accessTokens
# to receive your teamcity token.
teamcity-token = secret-token
```

Examples:
```bash
$ taxi-teamcity show
$ taxi-teamcity build schemas-testing
$ taxi-teamcity build backend-py3-testing -b archiving
```

### Teamcity run builds by raw **buildTypeId**
```bash
$ taxi-teamcity show --raw
$ taxi-teamcity raw-build YandexTaxiProjects_TaxiBackendPy3_Testing -b archiving
$ taxi-teamcity raw-build YandexTaxiProjects_Tools_Schemas_CustomTesting
```

### Teamcity aliases
Get your **buildTypeId** from
https://teamcity.taxi.yandex-team.ru or **show --raw** command.

Put extra aliases of buildTypeId to `~/.taxi-devtools.d/teamcity-aliases.yaml`:
```yaml
short-alias: buildTypeId
short-alias2:
   id: buildTypeId2
   branch: service-name2
```
Equivalent runs:
```bash
$ taxi-teamcity build short-alias -b service-name
$ taxi-teamcity raw-build buildTypeId -b service-name
```

Equivalent runs:
```bash
$ taxi-teamcity build short-alias2
$ taxi-teamcity build short-alias2 -b service-name2
$ taxi-teamcity raw-build buildTypeId2 -b service-name2
```
