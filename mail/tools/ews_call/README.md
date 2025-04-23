# Example usage

```
$ grep request /var/log/corba/calendar.web.exchange.json.log | head -1 | ./jsonlog2soap.py > /tmp/exchange.request.xml
$ ./ews-call -p <exchange login password> /tmp/exchange.request.xml
```

To obtain exchange passwords see property ```ews.mailbot2013.password``` in calendar admin page.
