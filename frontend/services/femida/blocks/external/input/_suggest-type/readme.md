<a name="module_input_suggest-type_femida-multiplesugglect"></a>

## input_suggest-type_femida-multiplesugglect ⇐ <code>BEM.DOM</code>
Инпут, в котором одновременно реализованы саджест и мультиселект
существенная часть реализации взята из input_suggest_yes

**Extends:** <code>BEM.DOM</code>  
**Author:** gescbnet  
**Example**  
```js
{
    block: 'input',
    value: this._field.caption,
    iconRight: {
        mods: {
            type: 'arrow'
        },
        direction: 'top'
    },
    mix: {
        block: this.block,
        elem: 'control'
    },
    mods: {
        suggest: 'yes',
        'suggest-type': 'femida-multiplesugglect',
        size: this.mods.size || 's',
        theme: 'normal',
        disabled: this._field.disabled ? 'yes' : ''
    },
    js: {
        dataprovider: this._field.dataprovider,
        showListOnFocus: true
    ,
    placeholder: this._field.placeholder,
    content: {
        elem: 'control'
    }
}
```
