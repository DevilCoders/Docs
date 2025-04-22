# Infra maintenance creator

### How to

We have common conf template in `porto.yaml` like name, description, duration. Other fields like location, percent,
duration can be defined/redefined by cmdline flags.

### Example

We want to deploy porto on 10% sas.

`./hmctl infra infra/porto.yaml --percent 10 --location SAS`

Or we want to deploy porto in 'default'.

`./hmctl infra infra/porto.yaml --duration 5h --location ALL`
