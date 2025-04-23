Java build wrapper
==================

A to-be-unified build wrapper for gradle-based projects for use in `ya package` .json's.

Installs JDK, Android SDK, runs given gradle tasks and outputs specified artifacts to the build dir.


Important:
* runs builds with disabled `external-builder` as it is to be run from `ya package` (external build artifacts can be passed via args)
* supports `product` property for gradle builds

**TODO**: not yet implemented:
* properly supporting `yandex_signer` (not clear if it is required in the wrapper itself)
