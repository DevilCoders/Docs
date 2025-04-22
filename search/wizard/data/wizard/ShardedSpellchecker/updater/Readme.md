Usage:

```
ya make -r
./updater
svn ci ..
rm -rf ../_new_data
```

The script will get the most recent spellchecker snapshot,
will place all the files where needed and update all begemot ya.make's.
All Spellchecker files will be uploaded to sandbox once again (via skynet)

The real solution will be devised here:
https://st.yandex-team.ru/MISSPELLDEV-157
