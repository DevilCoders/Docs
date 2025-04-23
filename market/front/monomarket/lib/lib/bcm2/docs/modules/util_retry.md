[BCM2](../README.md) / [Exports](../modules.md) / util/retry

# Module: util/retry

## Table of contents

### Type aliases

- [RetryDelay](util_retry.md#retrydelay)

### Functions

- [constantRetry](util_retry.md#constantretry)
- [exponentialRetry](util_retry.md#exponentialretry)
- [logariphmicRetry](util_retry.md#logariphmicretry)
- [manualRetry](util_retry.md#manualretry)
- [quadraticRetry](util_retry.md#quadraticretry)

## Type aliases

### RetryDelay

Ƭ **RetryDelay**: (`counter`: *number*, `error`: Error) => *number*

#### Type declaration:

▸ (`counter`: *number*, `error`: Error): *number*

#### Parameters:

Name | Type |
:------ | :------ |
`counter` | *number* |
`error` | Error |

**Returns:** *number*

Defined in: lib/lib/bcm2/src/util/retry.ts:1

## Functions

### constantRetry

▸ **constantRetry**(`delay`: *number*): [*RetryDelay*](util_retry.md#retrydelay)

Ретраи через постоянный заданный интервал

#### Parameters:

Name | Type |
:------ | :------ |
`delay` | *number* |

**Returns:** [*RetryDelay*](util_retry.md#retrydelay)

Defined in: lib/lib/bcm2/src/util/retry.ts:7

___

### exponentialRetry

▸ **exponentialRetry**(`base`: *number*, `scale`: *number*, `expBase`: *number*, `expScale`: *number*): [*RetryDelay*](util_retry.md#retrydelay)

Ретраи через экспоненциально возрастающие промежутки base + scale * expBase ^ (x * expScale)

#### Parameters:

Name | Type |
:------ | :------ |
`base` | *number* |
`scale` | *number* |
`expBase` | *number* |
`expScale` | *number* |

**Returns:** [*RetryDelay*](util_retry.md#retrydelay)

Defined in: lib/lib/bcm2/src/util/retry.ts:38

___

### logariphmicRetry

▸ **logariphmicRetry**(`base`: *number*, `scale`: *number*, `logBase`: *number*): [*RetryDelay*](util_retry.md#retrydelay)

Ретраи через логарифмически возрастающие промежутки base + scale * Log(logBase, logBase + x)

#### Parameters:

Name | Type |
:------ | :------ |
`base` | *number* |
`scale` | *number* |
`logBase` | *number* |

**Returns:** [*RetryDelay*](util_retry.md#retrydelay)

Defined in: lib/lib/bcm2/src/util/retry.ts:27

___

### manualRetry

▸ **manualRetry**(`delays`: *number*[], `rest`: *number*): [*RetryDelay*](util_retry.md#retrydelay)

Ретраи через заданные вручную промежутки

#### Parameters:

Name | Type |
:------ | :------ |
`delays` | *number*[] |
`rest` | *number* |

**Returns:** [*RetryDelay*](util_retry.md#retrydelay)

Defined in: lib/lib/bcm2/src/util/retry.ts:47

___

### quadraticRetry

▸ **quadraticRetry**(`a`: *number*, `b`: *number*, `c`: *number*): [*RetryDelay*](util_retry.md#retrydelay)

Ретраи через квадратично возрастающие промежутки ax^2 + bx + c

#### Parameters:

Name | Type |
:------ | :------ |
`a` | *number* |
`b` | *number* |
`c` | *number* |

**Returns:** [*RetryDelay*](util_retry.md#retrydelay)

Defined in: lib/lib/bcm2/src/util/retry.ts:17
