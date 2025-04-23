### Usage: chinit [options] [command]

#### chinit is a linux utility that allows to kill a process tree or, in another words, kill all child processes.

More exactly, chinit creates new pid namespace with 'init' process linked with caller.
If one of auxiliary processes terminated, than 'init' process terminates, so whole process tree terminates by kernel.
See man page or source code for more details.

### Example:
```bash
$ # without chinit, sleep became a zombie:
$ bash -c 'echo PID=$$; sleep 1.2345 &' && pgrep -f 'sleep 1.2345'
PID=709117
709118
$ # sleep is killed by kernel:
$ chinit bash -c 'echo PID=$$; sleep 1.2345 &' && pgrep -f 'sleep 1.2345'
PID=2
$ # as the previous one, but exec in 'init' directly to bash:
$ chinit --exec bash -c 'echo PID=$$; sleep 1.2345 &' && pgrep -f 'sleep 1.2345'
PID=1
```
