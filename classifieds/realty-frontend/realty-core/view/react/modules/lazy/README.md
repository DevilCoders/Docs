# Lazy
## Overview & Basic Example
This module is used to delay resources loading

`<ObserverProvider />` creates IntersectionObserver and provides Intersection
 API to the react context. Props are the same with IntersectionObserver
 
`<Lazy />` component provides "lazy" prop, that used to control resource loading
 - `wrappedComponent`: _(Component)_ - wrapped component
 - `propName`: _(string = 'lazy')_ - wrapped component prop name,
 - `onLoad`: _(func)_ - called when item is need to be loaded (`lazy === false`),
 
`loadOnInterception(options, observerOptions)` enhancer, allows to wrap your components
 - `options`: _(object)_ - accepts `propName` and `createObserver` _(default 
 = true)_ fields. If `createObserver === false` you should manually wrap your
  component with ObserverProvider   


Default usage (creates ObserverProvider). LazyImage will load it's content 
only when it become visible.
```js
import React from 'react';
...

const LazyImage = props => {
  const { lazy, src } = props
  
  return <img src={lazy ? 'placeholder.svg' : src} />
}
const LazyImageContainer = loadOnInterception()(LazyImage);

class App extends React.Component ({
  render() {
    return (
      ...
      <LazyImageContainer ...>
      ...
    );
  },
})

```

Advanced usage. There will be only 1 instance of IntersectionObserver.
```js
import React from 'react';
...

const LazyImage = props => {
  const { lazy, src } = props
  
  return <img src={lazy ? 'placeholder.svg' : src} />
}
const LazyImageContainer = loadOnInterception({ createObserver: false })(LazyImage);

class App extends React.Component ({
  render() {
    return (
      ...
      <ObserverProvider>
        <LazyImageContainer ...>
        <LazyImageContainer ...>
        <LazyImageContainer ...>
      </ObserverProvider>
      ...
    );
  },
})

```
