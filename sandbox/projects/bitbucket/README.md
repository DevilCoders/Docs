# Generic bitbucket sandbox tasks

## BUILD_PKG_FROM_GIT
- Fetch sources from git repo
- Exec {REPO}/build/sandbox/build.sh build script
### Task parameters
- container: [optional] resource id of LXC_CONTAINER type, you may create your own see [example](https://a.yandex-team.ru/arc/trunk/arcadia/tools/sandboxctl/examples/runtime-images/01-create-sandbox-lxc-image-with-docker-inside.yml)
- privileged: bool [optional] Should this container run in privileged mode
- ramdrive: int [optional] Create a RAM drive of specified size in GiB
- build_script: [optional] path to build script
- ref_id: refspec for git fetch
- repo_url: git repository URL
- vault_secret_name: Name of the sandbox vauld secret
- vault_secret_owner: User name who owns the secret
- vault_secret_user: Just set his value to "x-oauth-token"

### Build environment variables
- BUILD_RESOURCE_PATH: Directory there build script should place build artifacts
**TODO** Import webhook data as env
**TODO** Import gitref data as env

### Manual execution via [sandboxctl](https://a.yandex-team.ru/arc/trunk/arcadia//tools/sandboxctl/README.md)

```
 tools/sandboxctl create -W -i examples/01-build_pkg_from_git.yml
```

### Exec via commit hooks from (gobabygo)[https://gobabygo.n.yandex-team.ru/]
**TODO:**: Add description about hook integration

## BUILD_JUGGLER_CHECKS_BOUNDLE_GIT
**TODO:** add description for BuildJugglerChecksBundleGit
