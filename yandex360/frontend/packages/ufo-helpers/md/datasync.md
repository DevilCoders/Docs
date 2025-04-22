## Constants

<dl>
<dt><a href="#subscribeOnce">subscribeOnce</a> ⇒ <code>*</code></dt>
<dd><p>subscribes to db update only once</p>
</dd>
</dl>

## Functions

<dl>
<dt><a href="#openDatabase">openDatabase(params)</a> ⇒ <code>Promise.&lt;dataSyncApi.Database&gt;</code></dt>
<dd><p>Простая обёртка над <code>dataSyncApi.openDatabase</code>.</p>
</dd>
<dt><a href="#processRecord">processRecord(record)</a> ⇒ <code>Object</code></dt>
<dd><p>Превращает запись в простой объект с правильным преобразованием
полей по типам. Добавляет поля <code>collection_id</code> и <code>record_id</code>.</p>
</dd>
</dl>

## Typedefs

<dl>
<dt><a href="#DababaseUpdater">DababaseUpdater</a> : <code>function</code></dt>
<dd></dd>
<dt><a href="#DatabaseConnectionParams">DatabaseConnectionParams</a> : <code>object</code></dt>
<dd></dd>
</dl>

<a name="subscribeOnce"></a>

## subscribeOnce ⇒ <code>\*</code>
subscribes to db update only once

**Kind**: global constant  
**Returns**: <code>\*</code> - result of db.on method  

| Param | Type | Description |
| --- | --- | --- |
| database | <code>Object</code> | object |
| callback | <code>function</code> |  |

<a name="openDatabase"></a>

## openDatabase(params) ⇒ <code>Promise.&lt;dataSyncApi.Database&gt;</code>
Простая обёртка над `dataSyncApi.openDatabase`.

**Kind**: global function  

| Param | Type |
| --- | --- |
| params | <code>[DatabaseConnectionParams](#DatabaseConnectionParams)</code> | 

<a name="processRecord"></a>

## processRecord(record) ⇒ <code>Object</code>
Превращает запись в простой объект с правильным преобразованием
полей по типам. Добавляет поля `collection_id` и `record_id`.

**Kind**: global function  

| Param | Type |
| --- | --- |
| record | <code>dataSyncApi.Record</code> | 

<a name="DababaseUpdater"></a>

## DababaseUpdater : <code>function</code>
**Kind**: global typedef  

| Param | Type |
| --- | --- |
| db | <code>dataSyncApi.Database</code> | 

<a name="DatabaseConnectionParams"></a>

## DatabaseConnectionParams : <code>object</code>
**Kind**: global typedef  

| Param | Type | Default |
| --- | --- | --- |
| params.apiHost | <code>String</code> |  | 
| params.databaseId | <code>String</code> |  | 
| [params.collectionId] | <code>String</code> | <code>&#x27;&#x27;</code> | 
| [params.context] | <code>String</code> | <code>&#x27;app&#x27;</code> | 
| [params.onUpdate] | <code>DatabaseUpdater</code> |  | 

