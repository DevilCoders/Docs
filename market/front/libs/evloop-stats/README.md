# evloop-stats
Event loop statistics gathering module.

## API
### {void} start(name)
Start tracking with a name.

### {Stats} stop(name)
Stop tracking and returning current stats for a name. 

### Stats format
Identical to [bripkens/event-loop-stats](https://github.com/bripkens/event-loop-stats).

[See more](https://github.com/bripkens/event-loop-stats#property-insights)

## Example
```javascript
const evloopStats = require('@yandex-market/evloop-stats');

evloopStats.start('event_series1');
// series of interesting events…
const stats = evloopStats.stop('event_series1');
```
