## Runner

Runner is a simple http dev server that also can build JS bundles out of TS source
files. Roughly, it works as follows:

* `/out/vector.js` is considered a special path, for it runner build the engine, wraps
  workers into blob objects and concatenated result;
* if requested file has `.js` suffix *and* there's a TS file on the file system
  with the same name (e.g. `foo.js` requested and `foo.ts` exists), the runner
  will try to build JS bundle with `webpack` using the TS file as an entry point;
* or if there's a file on requested path, serve it;
* or if there's a directory on requested path, serve it's listing as HTML;
* or, if none of above, send 404.

Runner uses `express` and, as mentioned, `webpack`. `webpack` instances are cached
on per-entry base for performance.

Upon start the runner starts listen port `8080`. Custom port can be provided via
`PORT` environment variable.

If you want the runner to build a bundle suitable for a web worker, add `worker`
query paramter, e.g. `foo.js` (assuming that there's a `foo.ts`) would be a simple
bundle and `foo.js?worker` would be a worker bundle.

If you set `YENV=production` files for stands will be uglified and chache-control header will be set.
`YENV=production make dev`
