# Embed
### Мотивация этой доки
Embed (почти везде) внутри себя использует компонент `VideoSandbox`, в который пропсом `innerHtml` передается все его содержимое в виде строки.
Все, что вернет `renderToString(<VideoSandbox ...>)` на сервере, кладется в пропс `sandbox` и уже на клиенте вставляется в
iframe в методе `renderEmbedIframe`.  
Проблема заключается в том, что для Embed-ов одного типа содержимое практические идентично, за исключением
некоторых параметров, специфичных для конкретного вида Embed. Например, для `Embed_type_twitter` это параметры `id`, `type`, `params`.
Все содержимое Embed конкретного типа не хочется передавать по сети каждый раз, поэтому принцип его работы был немного переработан.

### Как теперь писать новые виды Embed
Вместо того, чтобы возвращать одну только JSX разметку содержимого Embed-а конкретного типа, нужно выделить в нем неизменяющуюся
часть. А в местах, где используется что-то динамическое, указать строковый литерал `"YA_TURBO_<название параметра>"`.

`<название параметра>` связано с тем, что будет лежать в динамических параметрах, и его 
стоит указывать в upper snake case.   

Адаптер Embed-а должен возвращать объект такого вида:  
```
{
    embed: ... // Разметка (шаблон) - неизменяющаяся от Embed-а к Embed-у часть его содержимого
    dataAttributes: { ... } // Динамические параметры
}
```  
Шаблон Embed-а конкретного типа кладется в redux store и используется чтобы получать результирующее содержимое. 

В объекте `dataAttributes` лежат динамические параметы, которые будут передаваться на клиент и подставляться в шаблон.
Ключи этого объекта можно указывать в kebab или snake case. Если значением ключа является объект,
то его следует передавать таким образом `encodeURIComponent(escapeHtml(JSON.stringify(object)))`. Это связано с тем,
что шаблон Embed проходит через вызов реактовского `renderToString` и `encodeURIComponent` в `VideoSandbox`. 

Например, пусть адаптер Embed-а возвращал такое содержимое:
```
<>
    <div id={params.id} />
    <script
        data-embed-id={params.id}
        data-type={params.subtype}
        data-params={JSON.stringify(embed)}
        dangerouslySetInnerHTML={{ __html: innerScript }}
    />
    <script
        async
        defer
        src={params.subtype === 'share' ? '//vk.com/js/api/share.js?151' : '//vk.com/js/api/openapi.js?151'}
    />
</>
```
Тогда новая его версия должна быть написана таким образом:
```
{
    embed: (
        <>
            <div id="YA_TURBO_EMBED_ID" />
            <script
                data-embed-id="YA_TURBO_EMBED_ID"
                data-type="YA_TURBO_TYPE"
                data-params="YA_TURBO_PARAMS"
                dangerouslySetInnerHTML={{ __html: innerScript }}
            />
            <script async defer src="YA_TURBO_SRC" />
        </>
    ),
    dataAttributes: {
        type: params.subtype,
        params: encodeURIComponent(escapeHtml(JSON.stringify(embed))),
        src: params.subtype === 'share' ? '//vk.com/js/api/share.js?151' : '//vk.com/js/api/openapi.js?151',
    },
}
```
