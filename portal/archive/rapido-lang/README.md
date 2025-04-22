Builds templates with inlined lang strings.
Finds all .view.js files, processes lang files and generates new variants of them.

## Installation

`npm i`

## Running

Directly: node run.js --config=<path to config>
rapido-lang will check `mtime` for all include files.
If main destination file (destView) would have bigger mtime rapido-lang will not do anything.

## Config file options

* sourcePath. Path to the source `*.view.js` file with template definitions.
* includePath. Directory, root for `INCLUDE` files.
* destDir. Path for generated files.
* destView. Path for the main generated file with all views.
* resultPrefix. Prefix for result files. Example: `desktop`.
* langFile. Path to json file with all translations.
* command. Command to be executed by WATCH.

In submodule mode requires options: `sourcePath` (for a proper error handling), `includePath`, `langFile`

## New files

Generates 2 files per available language: `<resultPrefix>.<lang>.lang.json` and `<resultPrefix>.<lang>.view.js`.
Languages list would be produced from the `<langFile>` file: all of them should be keys of the root object.
New templates would have special namespace `<lang>`.
Also generates `common` view file with templates without localization and main file with INCLUDES.

## Errors

Produces 4 type of errors:
* Cannot find string. Lang key is used, but doesn't present in the lang file.
* Cannot find node. Construction `smth.l10n("folder." + smth)` is used, but lang file doesn't contain the folder.
Doesn't provide info about subfolder keys.
* Lang value for key <key> should be string. In case of `[% l10n:array %]` usage, iview has no support for it.
* Cannot open INCLUDE file.

## Tests

`npm test`
