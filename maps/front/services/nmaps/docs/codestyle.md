# Codestyle

All following rules are mandatory for the new code. Existing codebase may violate them, but changes mustn't introduce new violations.

[Exports](#exports)

## Exports
All exports must be placed at the end of file and grouped in a single statement.

Good:
```ts
const CONST = 'value';

function func(): void {}

function func2(): void {}

class Cls {}

export {
    CONST,
    func,
    Cls
}
```

Bad:
```ts
export const CONST = 'value';

export function func(): void {}

function func2(): void {}

export class Cls {}
```

If module has a default export, it must be placed before the named ones.

Good:
```ts
export default Cls;
export {
    CONST,
    func
};
```

Bad:
```ts
export {
    CONST,
    func
};
export default Cls;
```

Reexport statements must be placed after the main export statements:
```ts
export default Cls;
export {
    CONST
    func
};
export { something } from './anotherModule';
```
