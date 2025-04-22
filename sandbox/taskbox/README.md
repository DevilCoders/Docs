## Local mode

```bash
# build
ya make --checkout taskbox/dispatcher projects/sandbox/bin
# run
SANDBOX_CONFIG=../etc/settings.yaml ./dispatcher/taskbox
```

Some usefull settings for local debug (set in `../etc/settings.yaml`):
```yaml
taskbox:
  dispatcher:
    use_subproc: True  # Use subprocess instead on Procman
    kill_workers_on_stop:  # Kill all workers on Taskbox stop
  worker:
    # Use this binary for all workers.
    # Useful if you don't want to run AgentR and upload resource to local Sandbox.
    tasks_binary: "{$ARCADIA_ROOT}/sandbox/projects/sandbox/sandbox-tasks"
```
