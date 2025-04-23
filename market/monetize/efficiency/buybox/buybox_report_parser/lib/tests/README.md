# Buybox_report_parser Tests

**How to run all tests?**

In directory `lib` make project with `-tA` option, for SVN:

```
ya make -r -tA --checkout
```

For ARC:

```
ya make -r -tA
```

**How to use resource with report response?**

You can use resource like in `test_price_after_cashback_and_randomization` test:
1. `resourse_str = resource.find("/response.json")` will give a string with the contents of `response.json`
2. Use `json.loads(resource_str)` to get json-dictionary object that can be passed into `parse_response` function (the main function of `buybox_report_parser`)

**How to get more recent resource?**

You can just run `update_response.py` program (all parameters should be fine by default):

```
python update_response.py
```

You also can specify parameters:
* `-q` - quiet mode, don't write info to the `stdout`. By default, information about pruning and target string length will be displayed.
* `-o` - output file. By default, output file will be `response.json` that is used in tests.
* `--msku` - msku to form the request. Should be on stock to get a useful response.

**What to pay attention for?**

Tests autochecking in Sandbox is not specified yet so before commit changes, run tests locally.

To run tests, make the project with `-tA` option:

```
ya make -r -tA --checkout
```

**Warning:** ensure `ya make` output has no `stderr` messages
 