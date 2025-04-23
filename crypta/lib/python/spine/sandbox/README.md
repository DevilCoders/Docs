## SandboxSchedulerGenerator
```python
# SandboxSchedulerGenerator requires JugglerCheckGenerator
juggler = CryptaYtCheckGenerator(host="host")

# Create generator with default Crypta parameters
sandbox = sandbox_scheduler.create_default_generator(juggler, ["TAG"])

# Create scheduler with 15 minute period, tasks will have 1 hour kill timeout
# Task must inherit CryptaTask for juggler checks to work properly
sandbox.create_scheduler(
    MyTask,
    kill_timeout=timedelta(hours=1),
    schedule_interval=timedelta(minutes=15),
    extra_params={
        "param1": "value1"
    },
    # Used both for juggler checks and as a parameter for MyTask 
    env=environment.STABLE,
).check(
    # CRIT when task did not have a successful finish for the last 2 hours
    crit_time=timedelta(hours=2),
)

sandbox.create_scheduler(
    backup.CryptaGraphHumanMatchingBackup,
    # do not start scheduler after creation
    start_immediately=False,
    # Do not create scheduler, instead update scheduler with the given id
    # Scheduler must have FIXED_ID tag
    scheduler_id=17848,
)

# Use TaskConfig for schedulers with multiple environments 
task_configs = [
    configs.TaskConfig(
        Task1,
        stable=configs.RunConfig(schedule_interval=timedelta(hours=1), kill_timeout=timedelta(hours=2)),
        testing=configs.RunConfig(schedule_interval=timedelta(hours=2), kill_timeout=timedelta(hours=2)),
    ),
    configs.TaskConfig(
        Task2,
        stable=configs.RunConfig(schedule_interval=timedelta(hours=2), kill_timeout=timedelta(hours=2)),
        testing=configs.RunConfig(schedule_interval=timedelta(hours=4), kill_timeout=timedelta(hours=2, minutes=30)),
    ),
]

# Create schedulers from TaskConfig, add juggler checks for stable environment only
for task_config in task_configs:
    for config in task_config:
        scheduler = sandbox.create_scheduler(**config.get_scheduler_config())
        if config.env == environment.STABLE:
            scheduler.check(timedelta(hours=16))
```
