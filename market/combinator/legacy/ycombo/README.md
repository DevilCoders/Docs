# Ycombo

## Description

Command line tool for easy interaction with combinator server by grpc requests.

## Setup

### Minimal setup

1. Download ycombo directory
   ```bash
   svn export svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/market/combinator/ycombo ; cd ycombo/
   ```

2. Activate environment
   ```bash
   source activate_venv.sh
   ```

3. Run ```ycomboclt```
   ```bash
   ycomboclt --test --pretty  courier-and-route-scenario
   ```

4. Enter ```deactivate``` to quit virtual environment.

## Usage

Just run ```ycomboclt``` and you'll see help.
Terminal autocomplete should work for ```ycomboclt``` command!
