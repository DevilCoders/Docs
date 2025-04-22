## UniRec для FreeSwitch

Демон подписывается на сообщения о звонках и формирует метаданные исходя из настроек dial plan.

### Configuration Example
```yaml
- hostname: <Имя ноды>
  node_settings:
    node_name: <Имя ноды>
    node_address: <адрес ноды>
    node_port: <порт Event Socket/8021>
    node_secret: <пароль Event Socket>
  required_events:
    Event-Name:
      - CHANNEL_HANGUP_COMPLETE
```
### XML DialPlan  Example

```xml
   <extension name="call_to_did" continue="true">
      <condition field="destination_number" expression="^(\d+)$" require-nested="false">
         <action inline="true" application="set" data="Guid=${sip_h_X-Cisco-Guid}" />
         <action inline="true" application="set" data="number_a=${caller_id_number}" />
         <action inline="true" application="set" data="number_b=${1}" />
      </condition>
   </extension>
```
Внутри dialplan необходимо объявить переменные, которые будут вычитаны в метаданные.

```json
{
	'number_a': '74959999999',
	'number_b': '61931',
	'Guid': '0497821568-0000065536-0008254450-4055002207',
	'call_duration': '0',
	'Event-Date-Timestamp': '1605701461426776'
}
```
