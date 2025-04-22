[BCM2](../README.md) / [Exports](../modules.md) / [http/transport](../modules/http_transport.md) / HttpTransportParseError

# Class: HttpTransportParseError

[http/transport](../modules/http_transport.md).HttpTransportParseError

## Hierarchy

* [*HttpTransportError*](http_transport.httptransporterror.md)

  ↳ **HttpTransportParseError**

## Table of contents

### Constructors

- [constructor](http_transport.httptransportparseerror.md#constructor)

### Properties

- [message](http_transport.httptransportparseerror.md#message)
- [requestId](http_transport.httptransportparseerror.md#requestid)
- [stack](http_transport.httptransportparseerror.md#stack)
- [statusCode](http_transport.httptransportparseerror.md#statuscode)
- [statusMessage](http_transport.httptransportparseerror.md#statusmessage)
- [url](http_transport.httptransportparseerror.md#url)
- [prepareStackTrace](http_transport.httptransportparseerror.md#preparestacktrace)
- [stackTraceLimit](http_transport.httptransportparseerror.md#stacktracelimit)

### Accessors

- [name](http_transport.httptransportparseerror.md#name)

### Methods

- [captureStackTrace](http_transport.httptransportparseerror.md#capturestacktrace)

## Constructors

### constructor

\+ **new HttpTransportParseError**(`request`: [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest), `error`: Error): [*HttpTransportParseError*](http_transport.httptransportparseerror.md)

#### Parameters:

Name | Type |
:------ | :------ |
`request` | [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest) |
`error` | Error |

**Returns:** [*HttpTransportParseError*](http_transport.httptransportparseerror.md)

Overrides: [HttpTransportError](http_transport.httptransporterror.md)

Defined in: lib/lib/bcm2/src/http/transport.ts:130

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
