Для всех callback'ов действует следующий контракт: URI - это
```python
ProdURI(
    uri=DatetimeURI(
        TablePath("//home/some_table", **range_args),
        date=datetime.datetime(**date_args)
    ),
    **control_flags
)
```
