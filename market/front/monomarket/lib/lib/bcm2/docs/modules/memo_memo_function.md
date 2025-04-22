[BCM2](../README.md) / [Exports](../modules.md) / memo/memo-function

# Module: memo/memo-function

## Table of contents

### Interfaces

- [CacheStorage](../interfaces/memo_memo_function.cachestorage.md)

### Type aliases

- [GetMemoKey](memo_memo_function.md#getmemokey)
- [GetMemoStorage](memo_memo_function.md#getmemostorage)
- [MemoFunction](memo_memo_function.md#memofunction)
- [Memoisable](memo_memo_function.md#memoisable)

### Variables

- [clearMemo](memo_memo_function.md#clearmemo)
- [dropMemo](memo_memo_function.md#dropmemo)
- [memoKey](memo_memo_function.md#memokey)
- [memoStorage](memo_memo_function.md#memostorage)

### Functions

- [memoFunction](memo_memo_function.md#memofunction)
- [memoisable](memo_memo_function.md#memoisable)

## Type aliases

### GetMemoKey

Ƭ **GetMemoKey**<Fn, Key\>: (...`args`: [*Arguments*](ts.md#arguments)<Fn\>) => Key

#### Type parameters:

Name | Type |
:------ | :------ |
`Fn` | [*AnyFn*](ts.md#anyfn) |
`Key` | - |

#### Type declaration:

▸ (...`args`: [*Arguments*](ts.md#arguments)<Fn\>): Key

#### Parameters:

Name | Type |
:------ | :------ |
`...args` | [*Arguments*](ts.md#arguments)<Fn\> |

**Returns:** Key

Defined in: lib/lib/bcm2/src/memo/memo-function.ts:23

___

### GetMemoStorage

Ƭ **GetMemoStorage**<Fn, Key\>: () => [*CacheStorage*](../interfaces/memo_memo_function.cachestorage.md)<Key, ReturnType<Fn\>\>

#### Type parameters:

Name | Type |
:------ | :------ |
`Fn` | [*AnyFn*](ts.md#anyfn) |
`Key` | - |

#### Type declaration:

▸ (): [*CacheStorage*](../interfaces/memo_memo_function.cachestorage.md)<Key, ReturnType<Fn\>\>

**Returns:** [*CacheStorage*](../interfaces/memo_memo_function.cachestorage.md)<Key, ReturnType<Fn\>\>

Defined in: lib/lib/bcm2/src/memo/memo-function.ts:24

___

### MemoFunction

Ƭ **MemoFunction**<Fn\>: Fn & { `[clearMemo]`: () => *void* ; `[dropMemo]`: (...`args`: [*Arguments*](ts.md#arguments)<Fn\>) => *void*  }

#### Type parameters:

Name | Type |
:------ | :------ |
`Fn` | [*AnyFn*](ts.md#anyfn) |

Defined in: lib/lib/bcm2/src/memo/memo-function.ts:31

___

### Memoisable

Ƭ **Memoisable**<Fn, KeyType\>: Fn & { `[memoKey]?`: [*GetMemoKey*](memo_memo_function.md#getmemokey)<Fn, KeyType\> ; `[memoStorage]?`: [*GetMemoStorage*](memo_memo_function.md#getmemostorage)<Fn, KeyType\>  }

#### Type parameters:

Name | Type | Default |
:------ | :------ | :------ |
`Fn` | [*AnyFn*](ts.md#anyfn) | - |
`KeyType` | - | *string* |

Defined in: lib/lib/bcm2/src/memo/memo-function.ts:26

## Variables

### clearMemo

• `Const` **clearMemo**: *typeof* [*clearMemo*](memo_memo_function.md#clearmemo)

Defined in: lib/lib/bcm2/src/memo/memo-function.ts:8

___

### dropMemo

• `Const` **dropMemo**: *typeof* [*dropMemo*](memo_memo_function.md#dropmemo)

Defined in: lib/lib/bcm2/src/memo/memo-function.ts:7

___

### memoKey

• `Const` **memoKey**: *typeof* [*memoKey*](memo_memo_function.md#memokey)

Defined in: lib/lib/bcm2/src/memo/memo-function.ts:4

___

### memoStorage

• `Const` **memoStorage**: *typeof* [*memoStorage*](memo_memo_function.md#memostorage)

Defined in: lib/lib/bcm2/src/memo/memo-function.ts:5

## Functions

### memoFunction

▸ **memoFunction**<Fn, Key\>(`fn`: [*Memoisable*](memo_memo_function.md#memoisable)<Fn, Key\>): [*MemoFunction*](memo_memo_function.md#memofunction)<Fn\>

Мемоизация функции

#### Type parameters:

Name | Type |
:------ | :------ |
`Fn` | [*AnyFn*](ts.md#anyfn) |
`Key` | - |

#### Parameters:

Name | Type |
:------ | :------ |
`fn` | [*Memoisable*](memo_memo_function.md#memoisable)<Fn, Key\> |

**Returns:** [*MemoFunction*](memo_memo_function.md#memofunction)<Fn\>

Defined in: lib/lib/bcm2/src/memo/memo-function.ts:50

___

### memoisable

▸ **memoisable**<Fn, Key\>(`getStorage`: [*GetMemoStorage*](memo_memo_function.md#getmemostorage)<Fn, Key\>, `getKey`: [*GetMemoKey*](memo_memo_function.md#getmemokey)<Fn, Key\>, `fn`: Fn): [*Memoisable*](memo_memo_function.md#memoisable)<Fn, Key\>

#### Type parameters:

Name | Type | Default |
:------ | :------ | :------ |
`Fn` | [*AnyFn*](ts.md#anyfn) | - |
`Key` | - | *string* |

#### Parameters:

Name | Type |
:------ | :------ |
`getStorage` | [*GetMemoStorage*](memo_memo_function.md#getmemostorage)<Fn, Key\> |
`getKey` | [*GetMemoKey*](memo_memo_function.md#getmemokey)<Fn, Key\> |
`fn` | Fn |

**Returns:** [*Memoisable*](memo_memo_function.md#memoisable)<Fn, Key\>

Defined in: lib/lib/bcm2/src/memo/memo-function.ts:97
