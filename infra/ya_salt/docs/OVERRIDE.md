## Why?
To perform long term experiments/debugging and other tricky local actions on host one may need to force `ya-salt`
to override external settings for one or multiple components. E.g.:
> SYSDEV team with ISS team want to debug LVM setup on one host for two+ weeks using custom diskmanager
> and ISS agent. But other components need to be managed by salt as usual.

## Mechanics
To perform that we use salt `PATH` mechanism, injecting `/etc/hostman/repo-override` as one of path items if it is
not empty.

## UX
Users can manually copy all or parts of salt repository into overrides directory, but we provide some tooling for that.
Namely:
  * `ya-salt override -n <name>` - which will copy contents of `common/{components,deploy}/<name>` allowing to modify it
  by user.
  * `ya-salt override -r -n <name>` - which will cleanup overrides for chosen component
Then on must edit interesting components using editor of choice.

## Monitoring
Having local overrides on hosts is bad for reliable fleet management, thus ya-salt monitors if we have local overrides
on host (i.e `/etc/hostman/repo-override` is not empty) and will set condition in `status.salt.overridden`:
```shell script
./ya-salt status -o json | jq .salt.overridden
{
  "message": "OK",
  "status": "True",
  "transitionTime": "2020-04-07T20:51:16.836811Z"
}

```