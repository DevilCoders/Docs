# tsum_events

tsum_events - library for sending events and microevents to tsum.

Usage:
```python
from market.pylibrary.tsum_events.tsum_events import Event, EventSender, EventStatus
event = MicroEvent(timeSeconds=1495723277, text="some text", type='salt', project='market', status=EventStatus.Value('WARN'), source='localhost', tags=['test', 'test2'])
sender = EventSender()
sender.send_micro_events(event)

event2 = MicroEvent(timeSeconds=1495723277, text="some text", type='salt', project='market', status=EventStatus.Value('WARN'), source='localhost', tags=['test', 'test2'])
events = MicroEvents()
events.expand([event, event2])
sender.send_micro_events(events)
```

Deb package: python-tsum-events

