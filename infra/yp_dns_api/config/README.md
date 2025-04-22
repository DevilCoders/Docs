# Configuration files for YP DNS API

YP DNS API consists of two components: Bridge and Replicator. Here are the configs for both of them.

## Bridge
There are two configs here:
- `bridge_prod_config.json` – config used in production
- `bridge_config.json` – config used for development and tests

Differences of dev config from production config:
1. sending logs to Unified Agent is disabled
2. using dev environment for dynamic zones management: dev YT paths are used, disabled instance registration, disabled configuration reports

## Replicator
- `replicator_config.json` – config used in production

**TODO**:
- Add dev config for Replicator
