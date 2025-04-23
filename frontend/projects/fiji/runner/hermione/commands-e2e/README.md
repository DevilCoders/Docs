## Functions

<dl>
<dt><a href="#yaSaveSendBeaconHistory">yaSaveSendBeaconHistory()</a> ⇒ <code>Promise</code></dt>
<dd><p>Складывает все запросы в sendBeacon в window.mm.beaconCounters</p>
</dd>
<dt><a href="#yaWaitBeaconCounter">yaWaitBeaconCounter(urlIncludes, [paramsIncludes])</a> ⇒ <code>Promise</code></dt>
<dd><p>Ожидает отправления RUM счетчика с нужными параметрами, не сработает если не вызван yaSaveSendBeaconHistory</p>
</dd>
</dl>

<a name="yaSaveSendBeaconHistory"></a>

## yaSaveSendBeaconHistory() ⇒ <code>Promise</code>
Складывает все запросы в sendBeacon в window.mm.beaconCounters

**Kind**: global function  
<a name="yaWaitBeaconCounter"></a>

## yaWaitBeaconCounter(urlIncludes, [paramsIncludes]) ⇒ <code>Promise</code>
Ожидает отправления RUM счетчика с нужными параметрами, не сработает если не вызван yaSaveSendBeaconHistory

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| urlIncludes | <code>String</code> \| <code>null</code> | подстрока которую нужно искать в урле отправленного счетчика |
| [paramsIncludes] | <code>String</code> | подстрока которую нужно искать в параметрах отправленного счетчика |

