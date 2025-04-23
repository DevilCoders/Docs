# app_runner

## cli
```
Usage: app_runner [OPTIONS] EXECUTABLE CMD OUTPUT [PARAMS]...

Options:
  --help  Show this message and exit.
```

## nirvana job-command
```
bash -c '${resource["app_runner"]} ${input["executable"]} --log=INFO run ${param["command"]} ${output["result"]} ${input["params"]}'
```

