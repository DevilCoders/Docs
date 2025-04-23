# `partial-lib-support`

## Configuration example

```js
// Allow/disallow whole d.ts.
'path/to/definition.d.ts': true
'path/to/definition.d.ts': false

'path/to/definition.d.ts': {
    // Allow/disallow everything from this d.ts, except for what is mentioned explictly.
    '*': true,
    '*': false,

    // Allow/disallow all methods on the type.
    TypeOrInterfaceOrClassName: true,
    TypeOrInterfaceOrClassName: false,

    // Allow/disallow specific methods on the type.
    SomeInterface: {
        // Allow/disallow all methods not mentioned explictly.
        '*': true,
        '*': false,

        // Explicitly allow/disallow method.
        method: true,
        method: false,

        // Allow method, but autmatically replace it with polyfill on build.
        //
        // `object.method(1, 2, 3)` will be replaced with
        //      `static: false` => `polyfillMethod(object, 1, 2, 3)`
        //      `static: true` => `polyfillMethod(1, 2, 3)`
        method: {name: 'methodPolyfill', file: './path/to/module-with-polyfills.ts', static: true}
    },

    // Allow/disallow specific globals (`declare var`) from d.ts.
    '@globals': {
        // Allow/disallow all globals not mentioned explictly.
        '*': true,
        '*': false,

        // Explicitly allow/disallow.
        global: true,
        global: false,

        // Allow global, but autmatically replace it with polyfill on build.
        //
        // `global` => `globalPolyfill`
        // `global.foo` => `globalPolyfill.foo`
        // `global.foo()` => `globalPolyfill.foo()`
        // `new global()` => `new globalPolyfill()`
        global: {name: 'globalPolyfill', file: './path/to/module-with-polyfills.ts'}
    }
}
```
