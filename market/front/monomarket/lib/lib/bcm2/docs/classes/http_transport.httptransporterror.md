[BCM2](../README.md) / [Exports](../modules.md) / [http/transport](../modules/http_transport.md) / HttpTransportError

# Class: HttpTransportError

[http/transport](../modules/http_transport.md).HttpTransportError

## Hierarchy

* *Error*

  ↳ **HttpTransportError**

  ↳↳ [*HttpTransportPrepareError*](http_transport.httptransportprepareerror.md)

  ↳↳ [*HttpTransportResponseError*](http_transport.httptransportresponseerror.md)

  ↳↳ [*HttpTransportRequestError*](http_transport.httptransportrequesterror.md)

  ↳↳ [*HttpTransportParseError*](http_transport.httptransportparseerror.md)

## Table of contents

### Constructors

- [constructor](http_transport.httptransporterror.md#constructor)

### Properties

- [message](http_transport.httptransporterror.md#message)
- [requestId](http_transport.httptransporterror.md#requestid)
- [stack](http_transport.httptransporterror.md#stack)
- [statusCode](http_transport.httptransporterror.md#statuscode)
- [statusMessage](http_transport.httptransporterror.md#statusmessage)
- [url](http_transport.httptransporterror.md#url)
- [prepareStackTrace](http_transport.httptransporterror.md#preparestacktrace)
- [stackTraceLimit](http_transport.httptransporterror.md#stacktracelimit)

### Accessors

- [name](http_transport.httptransporterror.md#name)

### Methods

- [captureStackTrace](http_transport.httptransporterror.md#capturestacktrace)

## Constructors

### constructor

\+ **new HttpTransportError**(`message?`: *string*): [*HttpTransportError*](http_transport.httptransporterror.md)

#### Parameters:

Name | Type |
:------ | :------ |
`message?` | *string* |

**Returns:** [*HttpTransportError*](http_transport.httptransporterror.md)

Inherited from: Error.constructor

Defined in: node_modules/typescript/lib/lib.es5.d.ts:978

## Properties

### message

• **message**: *string*

Inherited from: Error.message

Defined in: node_modules/typescript/lib/lib.es5.d.ts:974

___

### requestId

• **requestId**: *string*

Defined in: lib/lib/bcm2/src/http/transport.ts:78

___

### stack

• `Optional` **stack**: *string*

Inherited from: Error.stack

Defined in: node_modules/typescript/lib/lib.es5.d.ts:975

___

### statusCode

• `Optional` **statusCode**: *number*

Defined in: lib/lib/bcm2/src/http/transport.ts:72

___

### statusMessage

• **statusMessage**: *string*

Defined in: lib/lib/bcm2/src/http/transport.ts:74

___

### url

• **url**: *string*

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

Inherited from: Error.prepareStackTrace

Defined in: node_modules/@types/node/globals.d.ts:11

___

### stackTraceLimit

▪ `Static` **stackTraceLimit**: *number*

Inherited from: Error.stackTraceLimit

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

Inherited from: Error.captureStackTrace

Defined in: node_modules/@types/node/globals.d.ts:4
