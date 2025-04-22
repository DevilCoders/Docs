## Functions

<dl>
<dt><a href="#serialize">`serialize()`</a> ⇒ <code>Object</code></dt>
<dd><p>Сериализует форму</p>
</dd>
<dt><a href="#getSavedState">`getSavedState()`</a> ⇒ <code>String</code> | <code>null</code></dt>
<dd><p>Возвращает сохраненное состояние формы</p>
</dd>
<dt><a href="#dropSavedState">`dropSavedState()`</a></dt>
<dd><p>Сбрасывает сохраненное состояние формы</p>
</dd>
</dl>

## Events

<dl>
<dt><a href="#event_serialize">`"serialize" (data)`</a></dt>
<dd><p>Сериализация формы
Позволяет добавить форме дополнителньое поведение при сериализации</p>
</dd>
</dl>

<a name="serialize"></a>

## `serialize()` ⇒ <code>Object</code>
Сериализует форму

**Kind**: global function  
**Emits**: [<code>serialize</code>](#event_serialize)  
<a name="getSavedState"></a>

## `getSavedState()` ⇒ <code>String</code> \| <code>null</code>
Возвращает сохраненное состояние формы

**Kind**: global function  
<a name="dropSavedState"></a>

## `dropSavedState()`
Сбрасывает сохраненное состояние формы

**Kind**: global function  
<a name="event_serialize"></a>

## `"serialize" (data)`
Сериализация формы
Позволяет добавить форме дополнителньое поведение при сериализации

**Kind**: event emitted  

| Param | Type |
| --- | --- |
| data | <code>Object</code> | 

