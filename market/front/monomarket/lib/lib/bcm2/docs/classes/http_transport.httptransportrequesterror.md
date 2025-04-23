[BCM2](../README.md) / [Exports](../modules.md) / [http/transport](../modules/http_transport.md) / HttpTransportRequestError

# Class: HttpTransportRequestError

[http/transport](../modules/http_transport.md).HttpTransportRequestError

## Hierarchy

* [*HttpTransportError*](http_transport.httptransporterror.md)

  ↳ **HttpTransportRequestError**

## Table of contents

### Constructors

- [constructor](http_transport.httptransportrequesterror.md#constructor)

### Properties

- [message](http_transport.httptransportrequesterror.md#message)
- [requestId](http_transport.httptransportrequesterror.md#requestid)
- [stack](http_transport.httptransportrequesterror.md#stack)
- [statusCode](http_transport.httptransportrequesterror.md#statuscode)
- [statusMessage](http_transport.httptransportrequesterror.md#statusmessage)
- [url](http_transport.httptransportrequesterror.md#url)
- [prepareStackTrace](http_transport.httptransportrequesterror.md#preparestacktrace)
- [stackTraceLimit](http_transport.httptransportrequesterror.md#stacktracelimit)

### Accessors

- [name](http_transport.httptransportrequesterror.md#name)

### Methods

- [captureStackTrace](http_transport.httptransportrequesterror.md#capturestacktrace)

## Constructors

### constructor

\+ **new HttpTransportRequestError**(`request`: [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest), `error`: GotError): [*HttpTransportRequestError*](http_transport.httptransportrequesterror.md)

#### Parameters:

Name | Type |
:------ | :------ |
`request` | [*HttpTransportRequest*](../modules/http_transport_types.md#httptransportrequest) |
`error` | GotError |

**Returns:** [*HttpTransportRequestError*](http_transport.httptransportrequesterror.md)

Overrides: [HttpTransportError](http_transport.httptransporterror.md)

Defined in: lib/lib/bcm2/src/http/transport.ts:117

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
