## Catalogia tool

* Более подробно про опции смотрите `./catalogia --help`, можно указать пути к файлам модели, размер чанка и url web-каталогии.

* Категории печатаются в `stdout`

### Примеры

##### DSSM catalogia

```
sky get sbr:464321741 # or newer CATALOGIA_DSSM_MODEL resource
./catalogia --dssm # and print phrases to stdin and read categories from stdout
# or
./catalogia --dssm --file file_with_phrases.txt
```

##### Web catalogia

```
./catalogia
# or
./catalogia --file file_with_phrases.txt
```

