# Palmsync wrapper

## General information

Palmsync wrapper is a simple wrapper for [Palmsync tool](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/palmsync)

It cannot do much, but is suitable for simple tasks.

## Usage

`palmsync_wrapper <validate,synchronize,version> [--testpalm-token <testpalm_token>]`

## How to update this tool to new Palmsync version
https://wiki.yandex-team.ru/users/selivni/o-palmsyncwrapper/#obnovlenienanovujuversijupalmsync

## Mechanics

On launch, Palmsync wrapper does the following:
1. Extracts Node.JS and Palmsync into cache if it's not there already
2. Moves Palmsync (node_modules) either into CWD or right outside the reepository you're in
3. Sets up environment and launches Palmsync
4. Moves Palmsync back to the cache

## Updating

The updating process should be executed on two platforms: on Linux and Darwin.
How to update:
1. Download Node.JS archive. Darwin: https://nodejs.org/dist/v12.8.1/node-v12.8.1-darwin-x64.tar.gz, Linux: https://nodejs.org/dist/v12.8.1/node-v12.8.1-linux-x64.tar.gz
2. Extract the archive somewhere and do `export PATH=<node_path>/bin:$PATH`
3. Do `npm install @yandex-int/palmsync --registry https://npm.yandex-team.ru`. A node_modules directory should appear after successful inistallation.
4. Do `tar -cvzf palmsync.tar.gz node_modules`
5. Do `ya upload --ttl inf -d 'Palmsync vXX.X.XX x86_64 <Platform>' palmsync.tar.gz`
6. If Node.JS version has changed, repeat step 5 for downloaded archive
7. Change resource IDs at [maps/mobile/tools/palmsync_wrapper/ya.make](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/tools/palmsync_wrapper/ya.make)
8. Check that validaing/synchronizing still works properly
9. Review and commit your changes (note that all Palmsync checks are located at Testenv Jobs section, so they need to be launched manually)

## Packages

### Debian package
To fetch: `sudo apt-get update && sudo apt-get install yandex-maps-mobile-tools-palmsync-wrapper`

To upload to apt:
1. Launch YA_PACKAGE with package publishing enabled into `common` repository. An example: https://sandbox.yandex-team.ru/task/847069135
2. Ask khrolenko@ or vmazaev@ to push yandex-maps-mobile-tools-palmsync-wrapper to stable
