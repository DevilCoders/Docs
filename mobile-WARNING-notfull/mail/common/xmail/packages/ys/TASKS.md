## Things to do

### Statements:
* ~~declarations of `class` (methods, properties), `function`, `type`, `interface` (methods), `enum` (having raw values or without them), generics.~~
* ~~`import`~~
* ~~`Nullable` definition~~
*	~~`let`/`const` declarations~~
*	~~block statement (compound)~~
*	~~`if`, `if-else`~~
*	~~`return`~~. Need to figure out how to support labeled return in Kotlin.
*	~~`for-of`~~. Use `range` and `decrementalRange` to emulate `for (let i in 1..<10) {}`.
*	~~`break`~~
*	~~`continue`~~
*	~~`while`~~
*	~~`do-while`~~
*	~~`switch`~~

### Expressions:
*	~~Literals: number, string, array, Boolean, `null`, `undefined`~~
*	~~Variable access~~
*	~~Assignment (including compound): `=`, `+=`, `-=`, `*=`, `/=`, `%=`~~
*	~~Grouping (parentheses): `(a)`~~
*	~~Arithmetic: `+`, `-`, `*`, `/`, `%`, `<<`, `>>`, `>>>`, unary `-`, unary `+`~~
*	~~Comparison: `===`, `!===`, `==`, `!=`, `<`, `<=`, `>`, `>=`~~
*	~~Logical:  `&&`, `||`, `!`~~
*	~~Bitwise:  `&`, `|`, `~`, `^`~~
*	~~Ternary: `a ? b : c`~~
*	~~String `+`~~
*	~~`new`~~
*	~~Property access: `a.b`~~
*	~~Array access: `a[index]`~~
*	~~Call expression: `f()`~~
*	~~Arrow functions: `(a) => {}`~~
*	~~`this` inside functions~~
*	~~`instanceof`~~
*	~~`super` (access to predecessor)~~
* ~~`as`~~

### PAL injections:
* Design/implement a way to mark up PAL-injected interfaces (either a marker interface, or a decorator annotation)

### Implement Swift Generator
* ~~Add Reference-typed wrappers around standard collections. They are value types and will break Typescript code semantics.~~
* ~~Add Implementors for Standard types (see below in 'Standard types/objects')~~
* ~~Add Code Generation~~
* ~~Design and implement interface substitution mechanics (DI) for PAL~~

### Implement Kotlin Generator
* Package and import lists generation
* Add Implementors for Standard types (see below in 'Standard types/objects')
* Add Code Generation
* Design and implement interface substitution mechanics (DI) for PAL

### Standard types/objects:
* String: `length, concat, includes, startsWith, endsWith, indexOf, lastIndexOf, replace, substring, toUpperCase, toLowerCase, trim, trimLeft, trimRight, valueOf`
* Array: `from, length, push, pop, shift, unshift, sort, splice, concat, indexOf, lastIndexOf, join, slice, toString, filter, map, reduce, every, some, find, findIndex`
* Date: `get[Milliseconds/Seconds/Minutes/Hours/Days/Weeks/Months/Years], set[Milliseconds/Seconds/Minutes/Hours/Days/Weeks/Months/Years], toString, valueOf`
* Map: `length, clear, forEach, get, set, keys, values, delete`
* Math: `abs, sqrt, ceil, floor, round, trunc, max, min, random, pow`
* Number: `NaN, parseFloat, parseInt, isNaN, toString, valueOf`
* Set: `add, delete, clear, forEach, has, values`
