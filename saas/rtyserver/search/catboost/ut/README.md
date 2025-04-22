* To obtain rty_test.cbm for test: download the sandbox resource with the given ID (see ya.make) as models/rty_test.cbm. Alternatively, simply use ```ya make -tA``` to run tests.

* To rebuild (reproduce) rty_test.cbm 'from scratch':

```
./catboost fit --logging-level Verbose --learn-set train.tsv --column-description train.cd --loss-function Logloss -w 1 --depth 2 --iterations 100 --one-hot-max-size 10 --use-best-model
./catboost normalize-model -m model.bin --output-model model2.bin --print-scale-and-bias -i train.tsv --cd train.cd
./catboost calc -m model2.bin --input-path train.tsv --cd train.cd -o eval2.tsv --output-columns DocId,Target,RawFormulaVal
./model_ops convert -f CBM -t JSON model2.bin model.json

mv model2.bin rty_test.cbm
```
Should rty_test.cbm be changed, please update the file in two locations: ut/ya.make here, and the arcadia_tests_data repository.
