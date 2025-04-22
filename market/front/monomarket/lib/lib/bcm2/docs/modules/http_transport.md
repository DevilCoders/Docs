[BCM2](../README.md) / [Exports](../modules.md) / http/transport

# Module: http/transport

## Table of contents

### Classes

- [HttpTransport](../classes/http_transport.httptransport.md)
- [HttpTransportError](../classes/http_transport.httptransporterror.md)
- [HttpTransportParseError](../classes/http_transport.httptransportparseerror.md)
- [HttpTransportPrepareError](../classes/http_transport.httptransportprepareerror.md)
- [HttpTransportRequestError](../classes/http_transport.httptransportrequesterror.md)
- [HttpTransportResponseError](../classes/http_transport.httptransportresponseerror.md)

### Variables

- [HTTP\_RETRY\_SAFE\_CODES](http_transport.md#http_retry_safe_codes)
- [httpTransportAgents](http_transport.md#httptransportagents)
- [httpTransportDefaultOptions](http_transport.md#httptransportdefaultoptions)
- [protoRoot](http_transport.md#protoroot)

### Functions

- [agentConstructor](http_transport.md#agentconstructor)
- [isAgentOptions](http_transport.md#isagentoptions)
- [isHttpAgent](http_transport.md#ishttpagent)
- [isHttpsAgent](http_transport.md#ishttpsagent)

## Variables

### HTTP\_RETRY\_SAFE\_CODES

• `Const` **HTTP\_RETRY\_SAFE\_CODES**: (*string* \| *number*)[]

Defined in: lib/lib/bcm2/src/http/transport.ts:46

___

### httpTransportAgents

• `Const` **httpTransportAgents**: HttpTransportAgents

Defined in: lib/lib/bcm2/src/http/transport.ts:158

___

### httpTransportDefaultOptions

• `Const` **httpTransportDefaultOptions**: *Partial*<[*HttpTransportOptions*](http_transport_types.md#httptransportoptions)\>

Defined in: lib/lib/bcm2/src/http/transport.ts:143

___

### protoRoot

• `Const` **protoRoot**: *Root*

Defined in: lib/lib/bcm2/src/http/transport.ts:163

## Functions

### agentConstructor

▸ **agentConstructor**(`url`: *string*, `agent`: [*HttpTransportAgentOptions*](http_transport_types.md#httptransportagentoptions)): *null* \| (...`args`: *any*[]) => [*HttpAgent*](http_transport_types.md#httpagent) \| [*HttpsAgent*](http_transport_types.md#httpsagent)

#### Parameters:

Name | Type |
:------ | :------ |
`url` | *string* |
`agent` | [*HttpTransportAgentOptions*](http_transport_types.md#httptransportagentoptions) |

**Returns:** *null* \| (...`args`: *any*[]) => [*HttpAgent*](http_transport_types.md#httpagent) \| [*HttpsAgent*](http_transport_types.md#httpsagent)

Defined in: lib/lib/bcm2/src/http/transport.ts:210

___

### isAgentOptions

▸ **isAgentOptions**(`agent`: [*HttpTransportAgentOptions*](http_transport_types.md#httptransportagentoptions)): agent is HttpTransportAgentRawOptions

#### Parameters:

Name | Type |
:------ | :------ |
`agent` | [*HttpTransportAgentOptions*](http_transport_types.md#httptransportagentoptions) |

**Returns:** agent is HttpTransportAgentRawOptions

Defined in: lib/lib/bcm2/src/http/transport.ts:206

___

### isHttpAgent

▸ **isHttpAgent**(`agent`: [*HttpTransportAgentOptions*](http_transport_types.md#httptransportagentoptions)): agent is HttpAgent

#### Parameters:

Name | Type |
:------ | :------ |
`agent` | [*HttpTransportAgentOptions*](http_transport_types.md#httptransportagentoptions) |

**Returns:** agent is HttpAgent

Defined in: lib/lib/bcm2/src/http/transport.ts:198

___

### isHttpsAgent

▸ **isHttpsAgent**(`agent`: [*HttpTransportAgentOptions*](http_transport_types.md#httptransportagentoptions)): agent is HttpsAgent

#### Parameters:

Name | Type |
:------ | :------ |
`agent` | [*HttpTransportAgentOptions*](http_transport_types.md#httptransportagentoptions) |

**Returns:** agent is HttpsAgent

Defined in: lib/lib/bcm2/src/http/transport.ts:202
