## Intro: Python in Sandbox
All Sandbox services that aren't deployed in binary form, and also non-binary tasks, are launched inside the virtual environment based on Skynet Python.
The environment is deployed for each platform and component separately in form of a `.tar.gz` archive and consists of Python interpreter, a list of all installed packages and the packages themselves.
To deploy a new version of environment, one needs to:
1. Run a `BUILD_SANDBOX_DEPS_2` task and release it to the respective release tag.
2. Run a `BUILD_SANDBOX` task with the components to update environment for.

## Add a new platform to Sandbox
Until [SANDBOX-6893](https://st.yandex-team.ru/SANDBOX-6893) is closed, this requires quite a lot of actions:

1. Come up with a new platform's name (alias); it (almost) always takes a form of `{platform}_{OS family}_{OS version}_{commercial name}`, for example, `osx_10.14_mojave`, or `linux_ubuntu_10.04_lucid`.
1. Add the said short name to:
    - [`VENV_PACKAGES`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/deploy/base.py?rev=5668820#L26), deploy logic for a new version of OS.
    The archive's name is decided during Sandbox release building in [`fetch_environment_package()`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox/build_sandbox/__init__.py?rev=5530769#L1015).
    - [`__OS_TAGS`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/deploy/client.py?rev=5667000#L307), client tags setup;
    - [`ContainerPlatforms`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common/types/client.py?rev=r9291944#L614);
    - [`OS` client tags group](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common/types/client.py?rev=r9291944#L504);
    - [`PLATFORM_ALIASES`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common/platform/__init__.py?rev=r9199432#L15) mapping for full `platform.platform()` value to a short alias used in Sandbox (defined in paragraph 1);
    - [`PLATFORM_ALIAS_BINARY`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common/platform/__init__.py?rev=r9199432#L109) mapping to determine compatibility of binaries;
    - [`PLATFORM_TO_TAG`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common/platform/__init__.py?rev=r9199432#L134) mapping;
    - [`get_platform_alias()`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common/platform/__init__.py?rev=r9199432#L169) code;
    - [`UbuntuRelease`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox/sandbox_lxc_image/image.py?rev=5214025#L7) enumeration in LXC building task.
1. Build an environment for the new platform.

### Platform discovery logic
1. For every platform in input parameters, `BUILD_SANDBOX` looks up a `SANDBOX_DEPS` resource with the corresponding `platform` attribute.
2. During deploy (layout extraction stage, specifically), **all** virtual environments for this OS family are extracted.
2. Based on OS version, a service (for example, the task launcher aka `client`) [decides which environment is to be used](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/deploy/base.py#L232).

## Rebuild a virtual environment for a platform
### `BUILD_SANDBOX_DEPS_2` task
For platforms already supported by Sandbox, you want to run a `BUILD_SANDBOX_DEPS_2` task, which will launch a task for every platform specified and then wait for it.
Every child task runs this script you are reading `README.md` for.
A couple of things to note:
- Archives are duplicated: one is to be released in `prestable`, the other one is for `stable` release tag;
- Although produced by children, the archives are registered for a parent task;
- To release new versions of environments, release the task into the desired release tag; to reset release status, release to `cancelled`;
- The per-platform changelog is built by the parent task by either looking at output parameters of a child task, or by unpacking the environment and running `pip freeze` from it.

### `virtualenv-builder` (this script)
Read below for details, but to cut long story short, you need to:
- Build it by running `ya make --checkout` against this directory;
- **Run the `virtualenv-builder` executable;** if you are lost, ask for help:
```bash
./virtualenv-builder --help
```
- Upload the archive to Sandbox under `SANDBOX_DEPS` resource type and with certain attributes set:
  - `platform={short platform name, as discussed at the beginning}`
  - `version={svn revision of requirements.txt}`

## Build the environment from scratch
### Overview
If you are on the target host and have access to VCS, that's great!
Otherwise, you have to build it on another machine and copy over (use `sky share` or anything else that fits).
Do note that you may also need to copy certain Python packages sources if they are patched and differ from the upstream (see "Hacks" section).

### Build the program
This should be of no issue, assuming you are in the root of Arcadia working copy (both SVN and [arc](https://wiki.yandex-team.ru/arcadia/arc/docs/cli/) work) and it's in `$PATH`.
If you compile against a foreign platform, add the corresponding flag:
```bash
ya make --target-platform windows sandbox/scripts/tools/virtualenv-builder
```

### Hacks
This tool would be as simple as `pip install -r requir:ements.txt` if it hadn't been for a few required custom actions. See:
- [hacks.py](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/scripts/tools/virtualenv-builder/hacks.py?rev=5000887)
- [`on_execute()` method of `BUILD_SANDBOX_DEPS_2`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox/build_sandbox_deps_2/__init__.py?rev=5686670#L170)

The notorious example is MongoEngine package which is patched; you have to copy it from Arcadia and supply to `virtualenv-builder` via `--path` argument.

## Usage example
Typically, you want to run `BUILD_SANDBOX_DEPS_2` and see what happens, but in case you need to bootstrap a new host, you'd have to do the whole thing manually.
**Let's see how it goes for, say, a brand new OS X Mojave platform.**
> All actions performed below may require tweaking, as time goes and conditions may change!
When reading, add "As of now, ..." before every paragraph.

### Preparations
Macs are usually managed by a dedicated team of administrators, hence you cannot use SSH agent forwarding, as your SSH key is not allowed to be logged with.
This leaves you without Arcadia access, so we're in need of another machine:
```bash
white@sandbox-dev:~/arc/arcadia/sandbox/scripts/tools/virtualenv-builder$ ya make --target-platform darwin && sky share virtualenv-builder
Ok
rbtorrent:783dc30a6473e27c1fb4aca85b6a10d965e68e11
white@sandbox-dev:~/arc/arcadia/sandbox/scripts/tools/virtualenv-builder$ cd /tmp && svn export -q svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/contrib/python/mongoengine mongoengine && sky share mongoengine
rbtorrent:c51985217e36bd92a5e763bf5946d78c1cf33bbb
white@sandbox-dev:/tmp$ sky share requirements.txt
rbtorrent:e6e0dc9ef64b9351d337bde41b7c3e8518525a93
```

### Setup & execution
```bash
sandbox-serp-mac05:~ root# mkdir experiments && cd experiments
sandbox-serp-mac05:experiments root# sky get rbtorrent:783dc30a6473e27c1fb4aca85b6a10d965e68e11
sandbox-serp-mac05:experiments root# sky get rbtorrent:c51985217e36bd92a5e763bf5946d78c1cf33bbb
sandbox-serp-mac05:experiments root# sky get rbtorrent:e6e0dc9ef64b9351d337bde41b7c3e8518525a93
sandbox-serp-mac05:experiments root# ls
mongoengine		requirements.txt	virtualenv-builder
sandbox-serp-mac05:experiments root# ./virtualenv-builder -r requirements.txt --revision 5076562 --path mongoengine/
```

For every installation step, it says the names of packages and attempts to install them in the virtual environment, failing on the very first error.
Regardless of the result, you can examine logs of every step and the packing/compilation process:
```bash
sandbox-serp-mac05:experiments root# ls
mongoengine			requirements.txt		sandbox-venv.5076562.tar.gz	venv-workdir			virtualenv-builder
sandbox-serp-mac05:experiments root# ls venv-workdir/
logs			logs.out.log		requirements-final.txt	venv
```

### Share the output
Once virtual environment is built, you need to upload two copies of archive into Sandbox and release each with different release tag (stable/prestable).
Don't forget `platform` and `version` attributes!
- If you're lucky to have your Mac reachable from the other Sandbox hosts, use `sky share` with `REMOTE_COPY_RESOURCE` [(task example)](https://sandbox.yandex-team.ru/task/420823807/view):
```bash
sandbox-serp-mac05:experiments root# sky share sandbox-venv.5076562.tar.gz
rbtorrent:9db4721968ddea31ce07db9455cae7e6aaafb65d
```
- Otherwise, run [`ya upload`](https://wiki.yandex-team.ru/yatool/upload) from Arcadia root.
