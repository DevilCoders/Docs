[BCM2](../README.md) / [Exports](../modules.md) / [http/transport](../modules/http_transport.md) / HttpTransportPrepareError

# Class: HttpTransportPrepareError

[http/transport](../modules/http_transport.md).HttpTransportPrepareError

## Hierarchy

* [*HttpTransportError*](http_transport.httptransporterror.md)

  ↳ **HttpTransportPrepareError**

## Table of contents

### Constructors

- [constructor](http_transport.httptransportprepareerror.md#constructor)

### Properties

- [message](http_transport.httptransportprepareerror.md#message)
- [requestId](http_transport.httptransportprepareerror.md#requestid)
- [stack](http_transport.httptransportprepareerror.md#stack)
- [statusCode](http_transport.httptransportprepareerror.md#statuscode)
- [statusMessage](http_transport.httptransportprepareerror.md#statusmessage)
- [url](http_transport.httptransportprepareerror.md#url)
- [INCOMPATIBLE\_AGENT\_HTTP](http_transport.httptransportprepareerror.md#incompatible_agent_http)
- [INCOMPATIBLE\_AGENT\_HTTPS](http_transport.httptransportprepareerror.md#incompatible_agent_https)
- [RAW\_BODY\_TYPE\_NOT\_OBJECT](http_transport.httptransportprepareerror.md#raw_body_type_not_object)
- [RAW\_BODY\_TYPE\_NOT\_STRING](http_transport.httptransportprepareerror.md#raw_body_type_not_string)
- [prepareStackTrace](http_transport.httptransportprepareerror.md#preparestacktrace)
- [stackTraceLimit](http_transport.httptransportprepareerror.md#stacktracelimit)

### Accessors

- [name](http_transport.httptransportprepareerror.md#name)

### Methods

- [captureStackTrace](http_transport.httptransportprepareerror.md#capturestacktrace)

## Constructors

### constructor

\+ **new HttpTransportPrepareError**(`error`: Error): [*HttpTransportPrepareError*](http_transport.httptransportprepareerror.md)

#### Parameters:

Name | Type |
:------ | :------ |
`error` | Error |

**Returns:** [*HttpTransportPrepareError*](http_transport.httptransportprepareerror.md)

Overrides: [HttpTransportError](http_transport.httptransporterror.md)

Defined in: lib/lib/bcm2/src/http/transport.ts:92

## Properties

### message

• **message**: *string*

Inherited from: [HttpTransportError](http_transport.httptransporterror.md).[message](http_transport.httptransporterror.md#message)

Defined in: node_modules/typescript/lib/lib.es5.d.ts:974

___

### requestId

• **requestId**: *string*

Inherited from: [HttpTransportError](http_transport.httptransporterror.md).[requestId](http_transport.httptransporterror.md#requestid)

Defined in: lib/lib/bcm2/src/http/transport.ts:78

___

### stack

• `Optional` **stack**: *string*

Inherited from: [HttpTransportError](http_transport.httptransporterror.md).[stack](http_transport.httptransporterror.md#stack)

Defined in: node_modules/typescript/lib/lib.es5.d.ts:975

___

### statusCode

• `Optional` **statusCode**: *number*

Inherited from: [HttpTransportError](http_transport.httptransporterror.md).[statusCode](http_transport.httptransporterror.md#statuscode)

Defined in: lib/lib/bcm2/src/http/transport.ts:72

___

### statusMessage

• **statusMessage**: *string*

Inherited from: [HttpTransportError](http_transport.httptransporterror.md).[statusMessage](http_transport.httptransporterror.md#statusmessage)

Defined in: lib/lib/bcm2/src/http/transport.ts:74

___

### url

• **url**: *string*

Inherited from: [HttpTransportError](http_transport.httptransporterror.md).[url](http_transport.httptransporterror.md#url)

Defined in: lib/lib/bcm2/src/http/transport.ts:76

___

### INCOMPATIBLE\_AGENT\_HTTP

▪ `Static` **INCOMPATIBLE\_AGENT\_HTTP**: *string*= 'Incompatible Agent: http protocol must use HttpAgent instance'

Defined in: lib/lib/bcm2/src/http/transport.ts:90

___

### INCOMPATIBLE\_AGENT\_HTTPS

▪ `Static` **INCOMPATIBLE\_AGENT\_HTTPS**: *string*= 'Incompatible Agent: https protocol must use HttpsAgent instance'

Defined in: lib/lib/bcm2/src/http/transport.ts:92

___

### RAW\_BODY\_TYPE\_NOT\_OBJECT

▪ `Static` **RAW\_BODY\_TYPE\_NOT\_OBJECT**: *string*= 'Body type is not an object'

Defined in: lib/lib/bcm2/src/http/transport.ts:88

___

### RAW\_BODY\_TYPE\_NOT\_STRING

▪ `Static` **RAW\_BODY\_TYPE\_NOT\_STRING**: *string*= 'Body type is not a string, buffer or readable stream, and encoding set to \'raw\''

Defined in: lib/lib/bcm2/src/http/transport.ts:86

___

### prepareStackTrace

▪ `Static` `Optional` **prepareStackTrace**: (`err`: Error, `stackTraces`: CallSite[]) => *any*

Optional override for formatting stack traces

**`see`** https://v8.dev/docs/stack-trace-api#customizing-stack-traces

#### Type declaration:

▸ (`err`: Error, `stackTraces`: CallSite[]): *any*

#### Parameters:

Name | Type |
:------ | :------ |
`err` | Error |
`stackTraces` | CallSite[] |

**Returns:** *any*

Defined in: node_modules/@types/node/globals.d.ts:11

Inherited from: [HttpTransportError](http_transport.httptransporterror.md).[prepareStackTrace](http_transport.httptransporterror.md#preparestacktrace)

Defined in: node_modules/@types/node/globals.d.ts:11

___

### stackTraceLimit

▪ `Static` **stackTraceLimit**: *number*

Inherited from: [HttpTransportError](http_transport.httptransporterror.md).[stackTraceLimit](http_transport.httptransporterror.md#stacktracelimit)

Defined in: node_modules/@types/node/globals.d.ts:13

## Accessors

### name

• get **name**(): *string*

**Returns:** *string*

Defined in: lib/lib/bcm2/src/http/transport.ts:80

## Methods

### captureStackTrace

▸ `Static`**captureStackTrace**(`targetObject`: *object*, `constructorOpt?`: Function): *void*

Create .stack property on a target object

#### Parameters:

Name | Type |
:------ | :------ |
`targetObject` | *object* |
`constructorOpt?` | Function |

**Returns:** *void*

Inherited from: [HttpTransportError](http_transport.httptransporterror.md)

Defined in: node_modules/@types/node/globals.d.ts:4
