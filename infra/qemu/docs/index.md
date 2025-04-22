# qemu tools quick intro

## Get vmexec binaries
vmexec is available as ya tool vmexec
```
alias vmexec='ya tool vmexec'
```
## Build project from scratch
```
# Nothing fancy, just use ya make
ya make  .

# Or build it in sandbox via sandboxctl
sandboxctl -W  ya-make infra/qemu/vmexec/vmexec
```

