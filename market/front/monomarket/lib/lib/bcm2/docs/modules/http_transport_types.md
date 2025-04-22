[BCM2](../README.md) / [Exports](../modules.md) / http/transport-types

# Module: http/transport-types

## Table of contents

### Interfaces

- [HttpPhases](../interfaces/http_transport_types.httpphases.md)
- [HttpTransportProtoData](../interfaces/http_transport_types.httptransportprotodata.md)
- [HttpTransportProtoFileInfo](../interfaces/http_transport_types.httptransportprotofileinfo.md)
- [SerializableSimple](../interfaces/http_transport_types.serializablesimple.md)

### Type aliases

- [HttpAgent](http_transport_types.md#httpagent)
- [HttpTransportAgentOptions](http_transport_types.md#httptransportagentoptions)
- [HttpTransportAgentRawOptions](http_transport_types.md#httptransportagentrawoptions)
- [HttpTransportBody](http_transport_types.md#httptransportbody)
- [HttpTransportBodyEncoding](http_transport_types.md#httptransportbodyencoding)
- [HttpTransportBodyParsers](http_transport_types.md#httptransportbodyparsers)
- [HttpTransportOptions](http_transport_types.md#httptransportoptions)
- [HttpTransportParams](http_transport_types.md#httptransportparams)
- [HttpTransportPreparedStream](http_transport_types.md#httptransportpreparedstream)
- [HttpTransportRawResponse](http_transport_types.md#httptransportrawresponse)
- [HttpTransportRequest](http_transport_types.md#httptransportrequest)
- [HttpTransportResponse](http_transport_types.md#httptransportresponse)
- [HttpTransportResponseBody](http_transport_types.md#httptransportresponsebody)
- [HttpsAgent](http_transport_types.md#httpsagent)
- [QueryArrayFormat](http_transport_types.md#queryarrayformat)

### Variables

- [HTTP\_TRANSPORT\_BODY\_ENCODER\_FORM](http_transport_types.md#http_transport_body_encoder_form)
- [HTTP\_TRANSPORT\_BODY\_ENCODER\_JSON](http_transport_types.md#http_transport_body_encoder_json)
- [HTTP\_TRANSPORT\_BODY\_ENCODER\_PROTOBUF](http_transport_types.md#http_transport_body_encoder_protobuf)
- [HTTP\_TRANSPORT\_BODY\_ENCODER\_RAW](http_transport_types.md#http_transport_body_encoder_raw)
- [HTTP\_TRANSPORT\_BODY\_PARSER\_BUFFER](http_transport_types.md#http_transport_body_parser_buffer)
- [HTTP\_TRANSPORT\_BODY\_PARSER\_JSON](http_transport_types.md#http_transport_body_parser_json)
- [HTTP\_TRANSPORT\_BODY\_PARSER\_PROTOBUF](http_transport_types.md#http_transport_body_parser_protobuf)
- [HTTP\_TRANSPORT\_BODY\_PARSER\_RAW](http_transport_types.md#http_transport_body_parser_raw)
- [HTTP\_TRANSPORT\_BODY\_PARSER\_STREAM](http_transport_types.md#http_transport_body_parser_stream)

## Type aliases

### HttpAgent

Ƭ **HttpAgent**: HttpAgentNative \| HttpAgentKeepAlive

Defined in: lib/lib/bcm2/src/http/transport-types.ts:40

___

### HttpTransportAgentOptions

Ƭ **HttpTransportAgentOptions**: [*HttpTransportAgentRawOptions*](http_transport_types.md#httptransportagentrawoptions) \| [*HttpAgent*](http_transport_types.md#httpagent) \| [*HttpsAgent*](http_transport_types.md#httpsagent)

Defined in: lib/lib/bcm2/src/http/transport-types.ts:69

___

### HttpTransportAgentRawOptions

Ƭ **HttpTransportAgentRawOptions**: AgentOptions & { `keepAliveEnhanced?`: *boolean* ; `name`: *string*  }

Defined in: lib/lib/bcm2/src/http/transport-types.ts:68

___

### HttpTransportBody

Ƭ **HttpTransportBody**: *string* \| Buffer \| FormData \| Readable \| SerializableTree

Defined in: lib/lib/bcm2/src/http/transport-types.ts:65

___

### HttpTransportBodyEncoding

Ƭ **HttpTransportBodyEncoding**: *typeof* [*HTTP\_TRANSPORT\_BODY\_ENCODER\_RAW*](http_transport_types.md#http_transport_body_encoder_raw) \| *typeof* [*HTTP\_TRANSPORT\_BODY\_ENCODER\_JSON*](http_transport_types.md#http_transport_body_encoder_json) \| *typeof* [*HTTP\_TRANSPORT\_BODY\_ENCODER\_FORM*](http_transport_types.md#http_transport_body_encoder_form) \| *typeof* [*HTTP\_TRANSPORT\_BODY\_ENCODER\_PROTOBUF*](http_transport_types.md#http_transport_body_encoder_protobuf)

Defined in: lib/lib/bcm2/src/http/transport-types.ts:60

___

### HttpTransportBodyParsers

Ƭ **HttpTransportBodyParsers**: *typeof* [*HTTP\_TRANSPORT\_BODY\_PARSER\_RAW*](http_transport_types.md#http_transport_body_parser_raw) \| *typeof* [*HTTP\_TRANSPORT\_BODY\_PARSER\_BUFFER*](http_transport_types.md#http_transport_body_parser_buffer) \| *typeof* [*HTTP\_TRANSPORT\_BODY\_PARSER\_JSON*](http_transport_types.md#http_transport_body_parser_json) \| *typeof* [*HTTP\_TRANSPORT\_BODY\_PARSER\_PROTOBUF*](http_transport_types.md#http_transport_body_parser_protobuf) \| *typeof* [*HTTP\_TRANSPORT\_BODY\_PARSER\_STREAM*](http_transport_types.md#http_transport_body_parser_stream)

Defined in: lib/lib/bcm2/src/http/transport-types.ts:54

___

### HttpTransportOptions

Ƭ **HttpTransportOptions**: [*TransportOptions*](base_transport.md#transportoptions) & *Partial*<{ `acceptStatusCode`: (`statusCode`: *number*) => *boolean* ; `agent`: [*HttpTransportAgentOptions*](http_transport_types.md#httptransportagentoptions) ; `allowGetBody`: *boolean* ; `allowProtoUnknownValues`: *boolean* ; `decompress`: *boolean* ; `dnsLookupIpVersion`: *auto* \| *ipv4* \| *ipv6* ; `encodeBody`: [*HttpTransportBodyEncoding*](http_transport_types.md#httptransportbodyencoding) ; `encoding`: BufferEncoding ; `followRedirect`: *boolean* ; `headers`: HttpTransportHeaders ; `host`: *string* ; `onProtoVerifyError`: (`error`: *string*) => *void* ; `parseBody`: [*HttpTransportBodyParsers*](http_transport_types.md#httptransportbodyparsers) ; `pathname`: *string* ; `proxyHeaders`: *string*[] ; `query`: [*SerializableSimple*](../interfaces/http_transport_types.serializablesimple.md) ; `queryArrayFormat`: [*QueryArrayFormat*](http_transport_types.md#queryarrayformat) ; `queryKeepNull`: *boolean* ; `requestProto`: Type \| [*HttpTransportProtoFileInfo*](../interfaces/http_transport_types.httptransportprotofileinfo.md) ; `responseProto`: Type \| [*HttpTransportProtoFileInfo*](../interfaces/http_transport_types.httptransportprotofileinfo.md) ; `responseProtoOptions`: IConversionOptions ; `timeout`: *number*  }\>

Defined in: lib/lib/bcm2/src/http/transport-types.ts:71

___

### HttpTransportParams

Ƭ **HttpTransportParams**: [*TransportParams*](base_transport.md#transportparams) & *Partial*<{ `additional`: *Record*<string, any\> ; `allowGetBody`: *boolean* ; `allowProtoUnknownValues`: *boolean* ; `body`: [*HttpTransportBody*](http_transport_types.md#httptransportbody) ; `dnsLookupIpVersion`: *auto* \| *ipv4* \| *ipv6* ; `encodeBody`: [*HttpTransportBodyEncoding*](http_transport_types.md#httptransportbodyencoding) ; `followRedirect`: *boolean* ; `fullResponse`: *boolean* ; `headers`: HttpTransportHeaders ; `host`: *string* ; `method`: *GET* \| *POST* \| *PUT* \| *HEAD* \| *PATCH* \| *OPTIONS* \| *DELETE* ; `onProtoVerifyError`: (`error`: *string*) => *void* ; `parseBody`: [*HttpTransportBodyParsers*](http_transport_types.md#httptransportbodyparsers) ; `pathname`: *string* ; `proxyHeaders`: *string*[] ; `query`: [*SerializableSimple*](../interfaces/http_transport_types.serializablesimple.md) ; `requestProto`: Type \| [*HttpTransportProtoFileInfo*](../interfaces/http_transport_types.httptransportprotofileinfo.md) ; `responseProto`: Type \| [*HttpTransportProtoFileInfo*](../interfaces/http_transport_types.httptransportprotofileinfo.md) ; `responseProtoOptions`: IConversionOptions ; `timeout`: *number*  }\>

Defined in: lib/lib/bcm2/src/http/transport-types.ts:107

___

### HttpTransportPreparedStream

Ƭ **HttpTransportPreparedStream**: HttpTransportResponseCommon & { `body`: Readable ; `timings`: *Record*<string, any\>  }

Defined in: lib/lib/bcm2/src/http/transport-types.ts:156

___

### HttpTransportRawResponse

Ƭ **HttpTransportRawResponse**: HttpTransportResponseCommon & { `body`: Buffer ; `duration`: *number* ; `phases`: [*HttpPhases*](../interfaces/http_transport_types.httpphases.md)  }

Defined in: lib/lib/bcm2/src/http/transport-types.ts:150

___

### HttpTransportRequest

Ƭ **HttpTransportRequest**: [*TransportRequest*](../interfaces/base_transport.transportrequest.md) & { `options`: Options ; `parseBody`: *string* ; `url`: *string*  }

Defined in: lib/lib/bcm2/src/http/transport-types.ts:138

___

### HttpTransportResponse

Ƭ **HttpTransportResponse**: [*TransportResponse*](../interfaces/base_transport.transportresponse.md) & HttpTransportResponseCommon & { `body`: [*HttpTransportResponseBody*](http_transport_types.md#httptransportresponsebody) ; `parse`: *number* ; `phases`: [*HttpPhases*](../interfaces/http_transport_types.httpphases.md) ; `rawBody`: Buffer  }

Defined in: lib/lib/bcm2/src/http/transport-types.ts:161

___

### HttpTransportResponseBody

Ƭ **HttpTransportResponseBody**: *Record*<string, any\> \| *string* \| Buffer \| Readable

Defined in: lib/lib/bcm2/src/http/transport-types.ts:66

___

### HttpsAgent

Ƭ **HttpsAgent**: HttpsAgentNative \| HttpAgentKeepAlive.HttpsAgent

Defined in: lib/lib/bcm2/src/http/transport-types.ts:41

___

### QueryArrayFormat

Ƭ **QueryArrayFormat**: *bracket* \| *index* \| *comma* \| *none* \| *default*

Defined in: lib/lib/bcm2/src/http/transport-types.ts:33

## Variables

### HTTP\_TRANSPORT\_BODY\_ENCODER\_FORM

• `Const` **HTTP\_TRANSPORT\_BODY\_ENCODER\_FORM**: *form*

Defined in: lib/lib/bcm2/src/http/transport-types.ts:51

___

### HTTP\_TRANSPORT\_BODY\_ENCODER\_JSON

• `Const` **HTTP\_TRANSPORT\_BODY\_ENCODER\_JSON**: *json*

Defined in: lib/lib/bcm2/src/http/transport-types.ts:50

___

### HTTP\_TRANSPORT\_BODY\_ENCODER\_PROTOBUF

• `Const` **HTTP\_TRANSPORT\_BODY\_ENCODER\_PROTOBUF**: *protobuf*

Defined in: lib/lib/bcm2/src/http/transport-types.ts:52

___

### HTTP\_TRANSPORT\_BODY\_ENCODER\_RAW

• `Const` **HTTP\_TRANSPORT\_BODY\_ENCODER\_RAW**: *raw*

Defined in: lib/lib/bcm2/src/http/transport-types.ts:49

___

### HTTP\_TRANSPORT\_BODY\_PARSER\_BUFFER

• `Const` **HTTP\_TRANSPORT\_BODY\_PARSER\_BUFFER**: *buffer*

Defined in: lib/lib/bcm2/src/http/transport-types.ts:44

___

### HTTP\_TRANSPORT\_BODY\_PARSER\_JSON

• `Const` **HTTP\_TRANSPORT\_BODY\_PARSER\_JSON**: *json*

Defined in: lib/lib/bcm2/src/http/transport-types.ts:45

___

### HTTP\_TRANSPORT\_BODY\_PARSER\_PROTOBUF

• `Const` **HTTP\_TRANSPORT\_BODY\_PARSER\_PROTOBUF**: *protobuf*

Defined in: lib/lib/bcm2/src/http/transport-types.ts:46

___

### HTTP\_TRANSPORT\_BODY\_PARSER\_RAW

• `Const` **HTTP\_TRANSPORT\_BODY\_PARSER\_RAW**: *raw*

Defined in: lib/lib/bcm2/src/http/transport-types.ts:43

___

### HTTP\_TRANSPORT\_BODY\_PARSER\_STREAM

• `Const` **HTTP\_TRANSPORT\_BODY\_PARSER\_STREAM**: *stream*

Defined in: lib/lib/bcm2/src/http/transport-types.ts:47
