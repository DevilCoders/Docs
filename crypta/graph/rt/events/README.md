## Events

Input events which schema.
the library is used to describe event format in input log and provides 
auxiliary methods to pack and unpack events.

Events are used for communication between resharder and buzzard.

### How to declare a new log format
1. add protobuf message with log schema in folder protos
1. register new message type in [TEventMessage::EType](proto/types.proto) 
1. add cpp header for new message class to file messages.h 
