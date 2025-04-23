# Set empty line before export statement (empty-line-before-exports)

Supports save consistent format code for export statement. 


## Rule Details

Examples of **incorrect** code for this rule:

```js

const CONSTANT = 'constant';
export default constant;
```

Examples of **correct** code for this rule:

```js

const CONSTANT = 'constant';

export default constant;

```

### Options
Options allow you to specify whether there are empty lines between experts.
All options is boolean value. If this option is not set, the formatting rule is not applied, 
i.e. the linter does not check whether there are empty lines between the exports.

 - `emptyLineBetweenReexports` - check set empty line between reexport declaration.
 ```js
// affiliate/empty-line-before-exports: [2, {emptyLineBetweenReexports: true}]
export * from './a'

export * from './a'

// affiliate/empty-line-before-exports: [2, {emptyLineBetweenReexports: false}]
export * from './a'
export * from './a'
```
 - `emptyLineBetweenExports` - check set empty line between export declaration.
  ```js
 // affiliate/empty-line-before-exports: [2, {emptyLineBetweenExports: true}]
 export const a = 'a';

 export const b = 'b';

 // affiliate/empty-line-before-exports: [2, {emptyLineBetweenExports: false}]
 export const a = 'a';
 export const b = 'b';
 ```
 - `emptyLineBetweenExportType` - check set empty line between different export type.
 ```js
 // affiliate/empty-line-before-exports: [2, {emptyLineBetweenExports: true}]
 export {default as a} from './a';
 export {default as b} from './a';

 export * from 'b';
 export * from 'g';

 export const f = 'b';
 export const d = 'b';

 export default test;

 // affiliate/empty-line-before-exports: [2, {emptyLineBetweenExports: false}]
 export {default as a} from './a';
 export {default as b} from './a';
 export * from 'b';
 export * from 'g';
 export const f = 'b';
 export const d = 'b';
 export default test;
  ```
