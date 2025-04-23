[BCM2](../README.md) / [Exports](../modules.md) / [base/context](../modules/base_context.md) / Context

# Class: Context

[base/context](../modules/base_context.md).Context

Контекст выполнения запросов.

## Table of contents

### Constructors

- [constructor](base_context.context.md#constructor)

### Properties

- [debugData](base_context.context.md#debugdata)
- [debugLog](base_context.context.md#debuglog)
- [isDebug](base_context.context.md#isdebug)
- [request](base_context.context.md#request)

### Methods

- [storeDebug](base_context.context.md#storedebug)

## Constructors

### constructor

\+ **new Context**(`request`: *IncomingMessage*, `isDebug?`: *boolean*): [*Context*](base_context.context.md)

#### Parameters:

Name | Type | Default value |
:------ | :------ | :------ |
`request` | *IncomingMessage* | - |
`isDebug` | *boolean* | false |

**Returns:** [*Context*](base_context.context.md)

Defined in: lib/lib/bcm2/src/base/context.ts:22

## Properties

### debugData

• `Readonly` **debugData**: *object*= {}

Всяческие отладочные данные.

#### Type declaration:

Defined in: lib/lib/bcm2/src/base/context.ts:18

___

### debugLog

• `Readonly` **debugLog**: *any*[]= []

Отладочный лог различных событий.

Defined in: lib/lib/bcm2/src/base/context.ts:12

___

### isDebug

• `Readonly` **isDebug**: *boolean*= false

Defined in: lib/lib/bcm2/src/base/context.ts:22

___

### request

• `Readonly` **request**: *IncomingMessage*

Defined in: lib/lib/bcm2/src/base/context.ts:20

## Methods

### storeDebug

▸ **storeDebug**(`debugData`: *unknown*): *void*

Запись нового сообщения в отладочный лог

#### Parameters:

Name | Type |
:------ | :------ |
`debugData` | *unknown* |

**Returns:** *void*

Defined in: lib/lib/bcm2/src/base/context.ts:40
