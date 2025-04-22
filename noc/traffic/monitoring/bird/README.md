*NB*: set parseable time format in bird.conf (with full ISO date and timezone):

```
timeformat route "%F %T%z";
timeformat protocol "%F %T%z";
```

Why this exporter exists:

* There is [czerwonk/bird_exporter](https://github.com/czerwonk/bird_exporter), and it speaks 
  directly to the BIRD socket, but doesn't allow to limit exporter's permissions to only read
  the needed data.
* We potentially can have nice things like downtimes for particular host's BGP sessions.
