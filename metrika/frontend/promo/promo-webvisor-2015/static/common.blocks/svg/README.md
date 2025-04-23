# SVG block


## Usage

```javascript
//calling priv, inserted by <img> tag
blocks.exec('svg', data, {
    url: 'image.svg',
    fallback: 'image-fallback.png',
    type: 'image',
    width: 120,
    height: 120
})

//bemjson, inserted by <object> tag
{
    block: 'svg',
    url: 'image.svg',
    fallback: 'image-fallback.png',
    type: 'object',
    width: 64,
    height: 64
}

//calling priv, inserted by <svg> tag
blocks.exec('svg', data, {
    content: '<svg><rect x="0" y="0" width="64" height="64" /></svg>',
    fallback: 'image-fallback.png',
    type: 'raw',
    width: 64,
    height: 64
})
```

##Available types

 * image - by `<img>` tag.
 * object - by `<object>` tag
 * raw - used to insert raw svg

All of these types support fallback image given in `fallback` parameter.

**NOTE**: for `raw` type fallback image couldn't be resized.

##Dependecies

```javascript
{
    block: 'svg',
    elems: [ 'fallback' ], //for inserting as object
    mods: [ 'raw' ] //for inserting svg inline
}
```
