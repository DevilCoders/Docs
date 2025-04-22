[BCM2](../README.md) / [Exports](../modules.md) / memo/memo-methods

# Module: memo/memo-methods

## Table of contents

### Type aliases

- [MemoMethods](memo_memo_methods.md#memomethods)

### Variables

- [dontCache](memo_memo_methods.md#dontcache)

### Functions

- [memoMethods](memo_memo_methods.md#memomethods)

## Type aliases

### MemoMethods

Ƭ **MemoMethods**<O\>: { [Key in keyof O]: O[Key] extends function ? MemoFunction<O[Key]\> : O[Key]}

#### Type parameters:

Name | Type |
:------ | :------ |
`O` | *Record*<string, any\> |

Defined in: lib/lib/bcm2/src/memo/memo-methods.ts:47

## Variables

### dontCache

• `Const` **dontCache**: *typeof* [*dontCache*](memo_memo_methods.md#dontcache)

Defined in: lib/lib/bcm2/src/memo/memo-methods.ts:5

## Functions

### memoMethods

▸ **memoMethods**<O\>(`object`: O): [*MemoMethods*](memo_memo_methods.md#memomethods)<O\>

Мемоизация методов

#### Type parameters:

Name | Type |
:------ | :------ |
`O` | *Record*<string, any\> |

#### Parameters:

Name | Type |
:------ | :------ |
`object` | O |

**Returns:** [*MemoMethods*](memo_memo_methods.md#memomethods)<O\>

Defined in: lib/lib/bcm2/src/memo/memo-methods.ts:57
