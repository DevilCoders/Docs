# Converter

### encode/decode
```sh
$ ya make -r
$ ./converter -e sample_short.json > encoded_sample_short.json # encode
$ ./converter -d encoded_sample_short.json > copy_sample_short.json # decode
```

### load/print
```sh
$ ya make -r
$ ./converter -l ./sample_short.json -s ./storage                           # load storage
$ ./converter -l sample_short.json -p > copy_sample_short.json              # load and short print
$ ./converter -l sample_short.json -f > full.json                           # load and full print
$ ./converter -s ./storage/endpoints -b ./backup/endpoints -p > short.json  # load and short print
$ ./converter -l sample_short.json -f/-p -i > only_id_and_key.json          # load and print only id and key
```
