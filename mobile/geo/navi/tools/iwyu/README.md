## Prerequisites
 * Bazel
 * C++17-capable c++ compiler
 * Python

The recommended way to get bazel is to install [bazelisk](https://docs.bazel.build/versions/master/install-bazelisk.html).
Bazelisk will download the required version of bazel, so bazel upgrades and branch switching with it is seamless.

## Running include-what-you-use
`./iwyu.sh` is a convenience script that builds iwyu, runs it and applies its suggestions. `./iwyu.sh` needs at least one argument which is
a path to `compile_commands.json` file that cmake generates. Be aware that by default it runs the include-what-you-use tool using only 1 process, so
it is recommended to supply a flag like `--jobs 10` to speed things up.

After applying the suggestions, the script also runs `clang-format-diff.py` to fix the order of includes by taking the output of `arc diff`,
so any uncommited changes will be reformatted as well.
