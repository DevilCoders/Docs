Run `make clean build` in `solomon/j` directory before run this scripts.

Usage:

```
# dum table into text file
./dump_table.sh PROD_STP_MAN junk_kiwi_fol_hen_exports_30

# find out what to delete
grep '&host=kiwi612&' junk_kiwi_fol_hen_exports_30.txt > to_delete.txt

# check that you will delete only what you want
less to_delete.txt
wc -l to_delete.txt

# split into lables and ids
./split.sh to_delete.txt

# delete from MetaBase
./delete_from_metabase.sh PROD_STP_MAN junk_kiwi_fol_hen_exports_30 labels.txt

# delete from Stockpile
./delete_from_stockpile.sh PROD_STP_MAN ids.txt --force
```

There is a way to restore sensors meta (but not data in Stockpile) if you
accidentally delete more sensors than you want. Just keep dumped file and run:

```
./restore_in_metabase.sh PROD_STP_MAN junk_kiwi_fol_hen_exports_30 junk_kiwi_fol_hen_exports_30.txt
```
