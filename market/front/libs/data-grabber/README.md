# Web Data Grabber

Как это работает в Маркете: https://wiki.yandex-team.ru/users/lengl/market-data-grabber/

## Install

```bash
$ npm i
```

### CLI options and parameters

```bash
Params
  visitor list - show list of available visitors.

Example of params usage
  1. List of visitors:
    ./bin/dvg.js visitor list
  2. Help for visitor command:
    ./bin/dvg.js visitor --help

Options
[req]  --inputFile or -i - path of input tsv-file with URLs into first column.
       --outputFile or -o - path of output json-file. Default is ./results/<timestamp>_<testDomain>.json
       --url or -u - url for single visit. Result will be print to the stdout.
[req]  --testDomain or -t - domain of test resource.
       --controlDomain or -c - domain of test resource. Default is market.yandex.ru
[req]  --visitor - filename of visitor's script in './src/visitors/' directory.
       --screenshot - take screenshots of DOM-nodes. Default is false
       --useBase64 - attach screenshots as base64 string to result. If set to false, will save screenshot as a file instead. Default is true.
       --showBrowser - show browser's window. Default is false
       --pauseBrowser - browser will be paused after navigation. Default is 0 (sec)
       --viewPortSizes - browser window's size. Default is 1200,2560 (w,h)
       --skip - count (number) of rows for skipping. Default is 0
       --limit - max count (number) of rows for tsv-file transformation. Default is unlimited
       --verbose - print more info about process to the stdout. Default is false
       --silent - print to the stdout only results. Default is false
       --config - path to config file. CLI options will rewrite options from config file.
       --help or -h - print this help.

Examples of options usage
  1. From file to file:
    ./bin/dvg.js --inputFile=./tmp/yql_export.tsv --testDomain=market.yandex.ru --controlDomain=211142.market-exp.yandex.ru --verbose
  2. With another visitor (DOM-block):
    ./bin/dvg.js --url=/product--smartfon-apple-iphone-11-64gb/558171067 --testDomain=market.yandex.ru --visitor=km/top6
  3. Result to stdout:
    ./bin/dvg.js --url=/product--smartfon-apple-iphone-11-64gb/558171067 --testDomain=market.yandex.ru
  4. Result to stdout and without banners:
    ./bin/dvg.js --url=/product--smartfon-apple-iphone-11-64gb/558171067 --testDomain=market.yandex.ru --silent
  5. Result to stdout with browser's window and pause for 60 seconds:
    ./bin/dvg.js --url=/product--smartfon-apple-iphone-11-64gb/558171067 --testDomain=market.yandex.ru --showBrowser --pauseBrowser=60
```

## Examples

Configs could be managed by config file.

```bash
./bin/dvg.js \
       --config=./exampleConfig.js
```

### From `TSV`-file to `JSON`-file:
```bash
./bin/dvg.js \
       --inputFile=./tmp/yql_export.tsv \
       --outputFile=./path/to/file/here.json \
       --testDomain=211141.market-exp.yandex.ru \
       --controlDomain=211142.market-exp.yandex.ru \
       --verbose
```

### From `TSV`-file to `JSON`-file with limit and skip:
```bash
./bin/dvg.js \
       --inputFile=./tmp/yql_export.tsv \
       --outputFile=./path/to/file/here.json \
       --testDomain=211141.market-exp.yandex.ru \
       --controlDomain=211142.market-exp.yandex.ru \
       --skip=100 \
       --limit=10 \
       --verbose
```

### From `TSV`-file to `JSON`-file with browser's window:
```bash
       ./bin/dvg.js \
       --inputFile=./tmp/yql_export.tsv \
       --outputFile=./path/to/file/here.json \
       --testDomain=211141.market-exp.yandex.ru \
       --controlDomain=211142.market-exp.yandex.ru \
       --verbose \
       --showBrowser
```

### With another visitor (change target DOM-block):
```bash
./bin/dvg.js \
       --url=/product--smartfon-apple-iphone-11-64gb/558171067 \
       --testDomain=211141.market-exp.yandex.ru \
       --visitor=km/top6
```

### From `TSV`-file to `JSON`-file with custom viewport's size:
```bash
./bin/dvg.js \
       --inputFile=./tmp/yql_export.tsv \
       --testDomain=211141.market-exp.yandex.ru \
       --controlDomain=211142.market-exp.yandex.ru \
       --viewPortSizes=800,600 \
       --verbose
```

### Result of one request to stdout:
```bash
./bin/dvg.js \
       --url=/product--smartfon-apple-iphone-11-64gb/558171067 \
       --testDomain=211141.market-exp.yandex.ru
       --visitor=km/vizitka/main
```

### Result of one URL to stdout with screenshot:
```bash
./bin/dvg.js \
       --url=/product--smartfon-apple-iphone-11-64gb/558171067 \
       --testDomain=211141.market-exp.yandex.ru
       --visitor=km/do
       --screenshot
```

### Result of one URL to stdout without cli-banners:
```bash
./bin/dvg.js \
       --url=/product--smartfon-apple-iphone-11-64gb/558171067 \
       --testDomain=211141.market-exp.yandex.ru \
       --silent
```

### Show list of available visitors:
```bash
./bin/dvg.js visitor list
```
