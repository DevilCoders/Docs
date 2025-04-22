# Custom gun for Yandex Tank

A custom load generator for Yandex Tank. Read more on https://wiki.yandex-team.ru/Load/Pandora/.

## How to use

### Building for local debugging

```sh
# First cd into this directory
cd src/tools/stress/pandora

# Build and run
make
```

It will build the `pandora` binary and run it with the configuration from [conf.yaml](./conf.yaml). It's currently configured to shoot at `http://localhost:8080` target with ammo from [ammo-main.txt](./ammo-main.txt) and [ammo-jobs.txt](./ammo-jobs.txt).

### Building for release and using with Yandex Tank

If you made changes to the gun and want to use the new version in a shooting, you'll need to build the binary and upload it to Sandbox.

```sh
make upload-release
```

It will build the binary, upload it to Sandbox and print a download link (for example `https://proxy.sandbox.yandex-team.ru/2707151862`). Copy the new link and replace the `pandora.pandora_cmd` option of the [tank config](../../../../.configs/stress/load.yaml).

### Updating ammo files

You can upload modified ammo files to sandbox:

```sh
# main ammo
ya upload ammo-main.txt --do-not-remove
# or jobs ammo
ya upload ammo-jobs.txt --do-not-remove
```

and then replace the appropriate links under `pandora.resources` option of the [tank config](../../../../.configs/stress/load.yaml).
