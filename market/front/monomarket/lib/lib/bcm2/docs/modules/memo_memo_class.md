[BCM2](../README.md) / [Exports](../modules.md) / memo/memo-class

# Module: memo/memo-class

## Table of contents

### Type aliases

- [MemoedClass](memo_memo_class.md#memoedclass)

### Variables

- [MemoClass](memo_memo_class.md#memoclass)

### Functions

- [memoClass](memo_memo_class.md#memoclass)

## Type aliases

### MemoedClass

Ƭ **MemoedClass**<BaseClass\>: BaseClass & {}

#### Type parameters:

Name | Type |
:------ | :------ |
`BaseClass` | [*AnyClass*](ts.md#anyclass) |

Defined in: lib/lib/bcm2/src/memo/memo-class.ts:12

## Variables

### MemoClass

• `Const` **MemoClass**: [*MemoedClass*](memo_memo_class.md#memoedclass)<*typeof* BaseMemoClass\>

Класс с автоматической мемоизацией методов.

Defined in: lib/lib/bcm2/src/memo/memo-class.ts:29

## Functions

### memoClass

▸ **memoClass**<Class\>(`ClassDecl`: Class): [*MemoedClass*](memo_memo_class.md#memoedclass)<Class\>

Мемоизация методов класса

#### Type parameters:

Name | Type |
:------ | :------ |
`Class` | [*AnyClass*](ts.md#anyclass) |

#### Parameters:

Name | Type |
:------ | :------ |
`ClassDecl` | Class |

**Returns:** [*MemoedClass*](memo_memo_class.md#memoedclass)<Class\>

Defined in: lib/lib/bcm2/src/memo/memo-class.ts:22
