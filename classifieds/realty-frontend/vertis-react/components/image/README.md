## Overview & Basic Example
`<Image />` allows to use srcset (hi-res images for retina displays) 
 - `alt`: _(string)_ - img attr,
 - `children`: _(node)_ - if set component will render div instead of img 
 (pseudo mode),
 - `src`: _(string)_ - common src,
 - `srcX2`: _(string)_ - HD src,
 - `style`: _(object)_ - style prop,
 - `buildSrc`: _(func)_ - func that used to build final img src,
 - `buildStyle`: _(func)_ - func that used to build final style prop,
 - `isPseudo`: _(bool)_ - pseudo mode (not used when children is passed),
 
 
 `<LazyImage />` allows to use flag to control which image is rendered to dom 
  - `lazy`: _(bool)_ - placeholderSrc is used while this prop is true,
  - `srcPlaceholder`: _(string)_ - src for not loaded image


app.js
```js
import React from 'react';
import { StickyContainer, Sticky } from 'react-sticky';
...

class App extends React.Component ({
  render() {
    return (
      ...
      <Image
          className="GalleryImage"
          src={src}
          srcX2={srcX2}
          alt='Some text'
      />
      ...
    );
  },
});

```

### `<Image />` Props

#### buildSrc _(default: targetSrc => targetSrc)_ 
Used to build src prop, that passed down to img tag.
Accepts two arguments - src (based on deviceAspectRatio) and props of the 
`Image` component:

```js
<Image
    src={src}
    srcX2={srcX2}
    buildSrc={
        (targetSrc, props) => props.isSomeCondition ? targetSrc : props.otherSrc
    }
/>

```

#### buildStyle _(default: () => ({})_ 
Used to build style prop, that passed down to img\div tag.

_(Note: style is always passed to rendered tag,
 but if pseudo mode is active - style object will contain backgroundImage)_
 
Accepts two arguments - src (based on deviceAspectRatio) and props of the 
`Image` component:

```js
<Image
    src={src}
    srcX2={srcX2}
    buildSrc={
        (targetSrc, props) => ({ opacity: props.bar ? 1 : 0.2 })
    }
/>

```
