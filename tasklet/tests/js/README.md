To update JavaScript dependencies run
```
../../../serp/node_modules/bin/update-deps.py --list-paths-prefix '${ARCADIA_BUILD_ROOT}/tasklet/tests/js/' --npm-install-options='--no-bin-links'
```

The command above executes the `npm install`, uploads the `node_modules` directory as a resource to Sandbox using `ya upload` and your credentials, dumps the resource id to the `dependecies.inc` and the files list to the `dependecies.lst`.
