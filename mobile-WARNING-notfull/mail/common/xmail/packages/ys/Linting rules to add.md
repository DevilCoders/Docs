### Linting rules to add:
* Prohibit multiple assignments
* No `var`
* No use before declaration
* No function expressions
* No use of `||` or `&&` out of Boolean context, i.e. no `nullableVar || returnIfNull` or `nullableVar && doIfNotNull(nullableVar)` idiomatics.
* No indexing but with `number`
* Whitelist types: `Number`, `String`, `Boolean`, `Array`, `Map`, `Set`, `Date`. Prohibit use of `Number`, `String`, `Boolean` constructors.
* No `,` operator
* No multiple variables declaration in the same statement, i.e. no `let a = 'hello', b = 10`
* No parameter properties in class constructor

### Sample:
> adjacent-overload-signatures

> ban-comma-operator

> class-name

> curly

> no-arg

> no-conditional-assignment

> no-console

> no-debugger

> no-default-export

> no-duplicate-super

> no-duplicate-switch-case

> no-duplicate-variable

> no-dynamic-delete

> no-eval

> no-for-in-array

> no-inferred-empty-object-type

> no-invalid-this

> no-non-null-assertion

> no-parameter-properties

> no-require-import

> no-sparse-arrays

> no-use-before-declare

> no-var-keyword

> one-variable-per-declaration

> only-arrow-functions

> prefer-for-of

> restrict-plus-operands

> strict-boolean-expressions
