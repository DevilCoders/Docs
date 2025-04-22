## ReleaseGenerator

```python
import textwrap

from crypta.lib.python import crypta_env
from crypta.lib.python.spine import arcadia_ci

release_generator = arcadia_ci.ReleaseGenerator(
    # project_title="My project"  # passed to releases created from this generator
)

# Build -> testing -> stable (manual release)
release_registry = release_generator.standard_release(
    title="My release",
    abs_paths=["my/project/path/**"],
    # project_title="My project", # Used for grouping releases into files, by default equals to title
    # auto_stable=True,           # Use if for automatic release to stable
)


# Build docker image with CRYPTA_DOCKER resource via YA_PACKAGE_2
# https://a.yandex-team.ru/arcadia/ci/registry/projects/crypta/ya_package_docker.yaml
release_registry.add_docker_image("my/project/path/service/docker/ya-package.json")

# Build CRYPTA_UNIVERSAL_BUNDLE resource via YA_PACKAGE_2
# https://a.yandex-team.ru/arcadia/ci/registry/projects/crypta/ya_package.yaml
job = release_registry.add_universal_bundle("my/project/path/service/bundle/my-bundle-id.json")

# By default bundle name equals to file name
assert "my-bundle-id" == job.bundle_id


# Release that runs a single command
# https://a.yandex-team.ru/arcadia/ci/registry/common/misc/run_command.yaml
release_generator.run_cmd_release(
    title="Execute my command",
    abs_paths=["my/project/cmd/path/**"],
    cmd=textwrap.dedent("""
        ./ya make my/project/cmd/path/bin --stat
        my/project/cmd/path/my_command
    """)
# Add secret to environment
).run_job.add_secret(
    crypta_env.my_secret
)
```

## How to update a.yaml

```shell
ya make crypta/spine/pushers/arcadia_ci/test -AZ

# a.yaml files are located in crypta/spine/pushers/arcadia_ci/test/canondata
```
