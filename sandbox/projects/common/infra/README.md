# Collection of resunable general purpose sandbox tasks
## Features
- ==Reusable==
Once written each task may be reused w/o reinventing the wheel
- ==Collection of bricks ready to use==
User may implement his logic by combining tasks to form desired workflow
- ==No python coding requires==
User implements implement actual tasks logic via task body provided from arguments (usually via script)
- ==Rich collection of examples==
The only sandbox tasks which has examples, see [examples](./examples/)


## Try it with sandboxctl
Sandboxctl is tool to run sandbox tasks from comandline done right [home page](../../../../tools/sandboxctl/README.md)
```
cd $ARCADIA_ROOT/tools/sandboxctl/
ya make  .
cp bin/sandboxctl /usr/local/bin/
cd sandbox/projects/common/infra/
sandboxctl -W -i examples/01-exec_script.yaml
```
