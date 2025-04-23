# cmd interface for tvm qloud daemon

Add configuraton(s):
```
tvmtool add --src test:12 --dst 11:test1,14:test2,17:test5 --secret "test" --config ./config.json
```

Run the tool:
```
tvmtool --port 17 --config ./config.json
```
