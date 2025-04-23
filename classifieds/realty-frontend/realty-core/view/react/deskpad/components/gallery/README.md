## Overview & Basic Example
`<Gallery />` allows to quick preview set of images 
 - `children`: _(node|func|Array[node|func])_ - components that will be 
 render on top of the gallery (see details below),
 - `aspectRatioHolder`: _(string)_ - image that will hold preferred aspect 
 ratio,
 - `images`: _(Array<{ src: string, srcX2: string }>)_ - array of srcsets for
  `Image` component,
 - `limit`: _(number)_ - maximum amount of images that will be rendered to 
 gallery,
 - `total`: _(number)_ - total amount of images for this item,
 - `renderItem`: _(func)_ - usually returns gallery Image item (see details 
 below)


app.js
```js
import React from 'react';
import { StickyContainer, Sticky } from 'react-sticky';
...

class App extends React.Component ({
  render() {
    return (
      ...
      <Gallery
          className={cn('SerpItem', 'gallery')}
          aspectRatioHolder={emptySmallImage}
          images={appSmallSnippetImages.map((src, idx) => ({
              src,
              srcX2: appLargeSnippetImages[idx]
          }))}
          total={totalImages}
          limit={4}
      >
          {childProps => {
               const { activeIdx, limit, total } = childProps;
           
               return (
                   <AbsoluteContent key='bullets' horizontal={horizontal} vertical={vertical}>
                       <BulletIndicator
                           current={activeIdx}
                           limit={limit}
                           total={total}
                       />
                   </AbsoluteContent>
                )
          }
      </Gallery>
      ...
    );
  },
});

```

### `<Gallery />` Props

#### children _(default: none)_ 
This components will be rendered on top of the gallery image.
It can be function or just a node, or mix of both:
```js
childProps => {
    const {
        activeIdx,
        src,
        srcX2,
        images,
        total,
        limit
    } = childProps;
    
    return (
        <div>...</div>
    )
}
``` 

```js
<Gallery
    className={cn('SerpItem', 'gallery')}
    aspectRatioHolder={emptySmallImage}
    images={[
        { src: '...', srcX2: '...' },
    ]}
    total={totalImages}
    limit={4}
>
      {childProps => {
           const { activeIdx, limit, total } = childProps;
       
           return (
               <AbsoluteContent key='bullets' horizontal={horizontal} vertical={vertical}>
                   <div>Some stuff</div>
               </AbsoluteContent>
            )
      }
       <AbsoluteContent key='price' horizontal='left' vertical='bottom'>
           <div>Some component</div>
       </AbsoluteContent>
</Gallery>

```

#### renderItem _(default: defaultRenderItem)_ 
It renders gallery item (usually image).
 
Default values is:
```js
const defaultRenderItem = props => {
    return (
        <GalleryImage {...props} />
    );
}
```

`props` is an object with these fields:
```js
renderItem({
    key,
    idx,
    src,
    srcX2,
    onMouseOver,
})
```

#### aspectRatioHolder _(default: undefined)_ 
Usually you can put svg as data-url.


```xml
<svg xmlns="http://www.w3.org/2000/svg" width="24" height="22" viewBox="0 0 24 22">
    <path fill="#FFF" fill-rule="evenodd" d="M17.151 3h3.858A2.997 2.997 0 0 1 24 6v13c0 1.664-1.34 3-2.991 3H2.99A2.997 2.997 0 0 1 0 19V6c0-1.664 1.34-3 2.991-3H6.85L9 0h6l2.151 3zm-1.027 2L14 2h-4L7.876 5H2.99A.991.991 0 0 0 2 6v13c0 .552.447 1 .991 1H21.01c.55 0 .991-.442.991-1V6c0-.552-.447-1-.991-1h-4.885zM12 17a5 5 0 1 1 0-10 5 5 0 0 1 0 10zm0-2a3 3 0 1 0 0-6 3 3 0 0 0 0 6z"/>
</svg>
```

```js
import emptySmallImage from '!svg-url-loader?noquotes!emptySmall.svg';

<Gallery
    aspectRatioHolder={emptySmallImage}
    ...
/>

```
