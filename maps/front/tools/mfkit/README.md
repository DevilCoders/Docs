# mfkit

Toolkit for maps frontend.

## Production using

`ya tool mfkit`

## Commands

[idm](./docs/idm.md)

## Developing

```
# terminal 1
npm run watch
# terminal 2
node ./out/bin/mfkit.js help
```


## Ya tool

- `ya tool mfkit` building for linux and mac for x86_64
- `ya tool mfkit` updating one time per day
- `ya tool mfkit --force-update` -  extra check for the latest version
- `ya tool mfkit --force-refetch` - completely clear the catalog with the tool and bring it back again
- There are special [resource type](https://a.yandex-team.ru/arcadia/sandbox/projects/maps/MapsFrontend/maps_front_toolkit) in sandbox for ya tool
