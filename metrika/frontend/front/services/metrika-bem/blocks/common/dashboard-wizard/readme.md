This dir has tools for creating wizard data
# wizard-tree.json
complete tree of wizard. It used for `tjson.json` `wizard-preset.json` and `wizard-levels.json`
 * edit `wizard.json` and `quality-metrics.json`
 * run
```bash
$ node tools/dashboard-wizard/create-wizard-tree.js
```

# tjson.json
used for create keyset in tanker
 * run
```bash
$ node tools/dashboard-wizard/create-tjson.js
```
 * upload `tools/dashboard-wizard/tjson.json` on [Tanker](http://tanker.yandex-team.ru/keys/?project-id=metrika-bem&keyset-id=blocks%3Acommon%3Adashboard-wizard&branch-id=master&perpage-count=100500)

# wizard-levels.json and wizard-presets.json
`wizard-levels.json` data for wizard selector
`wizard-preset.json` widget presets
 * run
```bash
$ node tools/dashboard-wizard/create-preset.js
```
