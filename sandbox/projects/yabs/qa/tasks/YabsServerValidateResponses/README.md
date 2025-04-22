## Testing 

## Testing sandbox task
For convenient task testing use `setup-sandbox` script – it sets up sandbox and adds all needed resources.
To stop and cleanup sandbox use `stop-sandbox` script. 

*NOTE:* scripts expect `sandox` executable to be at `~/arcadia/sandbox/sandbox`.

### Testing JSON validation
JSON validation and JSON beautifier utilities are covered with unit-tests. Run tests with
```bash
PYTHONPATH="$PYTHONPATH:/skynet" pytest tests
```
