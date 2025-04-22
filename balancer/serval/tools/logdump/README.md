logdump
=======

Streamed-tree event log parser. Dumps data in a TSV format: time, parent id, subtree id, event type, arguments. For leaf events, subtree id is 0; for roots, parent id is 0. Unknown event types are denoted as `?N' with no arguments.

Usage
-----

```
logdump [OPTIONS] <file>
```

Options
-------

**-s|--start-time TIME**: Left bound (inclusive) of the interval the events in which to output. Formats:

 * ISO 8601 (%Y-%m-%dT%H:%M:%S.%uZ, %Y-%m-%dT%H:%M:%SZ, or %Y-%m-%d);
 * Unix (floating point seconds, integer seconds, integer microseconds).

Note: if events are severely out-of-order, some of them may be dropped (e.g. if `PushAt` was used to insert a frame far in the past/future).

**-e|--end-time TIME**: Right bound (exclusive) of the interval; see above.

**-n|--frame-id TREE**: Only output the event with the specified id and its descendants. Note: when combined with -s, if the event itself is not in the interval, but some of its descendants are, they may not be printed.

**-i|--event-list TYPES**: Comma-separated list of event types to output, as names or IDs.

**-x|--exclude-list TYPES**: Comma-separated list of event types to ignore.

**-t|--tree**: Print the children of each event directly after it, and visualize the tree. Note: when combined with -s, -i, or -x, events that are children of those that are not shown are displayed as roots.
