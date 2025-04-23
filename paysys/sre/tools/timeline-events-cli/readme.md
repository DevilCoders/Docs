# timeline-events

Cli for python-timeline-events

usage examples:

```bash
timeline-events  --env=testing event title="Test event" status=WARN type="unknown" project="pricelabs" tags=cli:test,cli:test2 source=local startTimeSeconds="2017-05-26 12:34:56+03:00" endTimeSeconds=`date --rfc-3339=seconds` text="some text"
```

minimal usage(required fields generate automagically):

```bash
timeline-events microevent
```

