# timeline_events

timeline_events - library for sending events and microevents to timeline. Adapter for tsum_events library

Usage:
```python
from market.pylibrary.tsum_events.tsum_events import EventStatus, MicroEvents, MicroEvent, Event
from timeline_events import EventSender
import uuid

sender = EventSender(endpoint="https://timeline-test.paysys.yandex-team.ru")
event = Event(startTimeSeconds=1525435424, text="some text", type='program', project='test',
    status=EventStatus.Value('WARN'), source='iandreyev', tags=['test', 'test2'], id=uuid.uuid4().hex)
sender.send_events(event)

```

Deb package: python-timeline-events

