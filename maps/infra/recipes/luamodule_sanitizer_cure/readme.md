## Fix for lua modules tests running with sanitizers

Sanitizers in EXECTESTs of C/C++ lua modules spill multiple leak messages and incomprehensible backtraces with `<unknown module>` lines.  
These false-positive leaks detected for all static data in a module's shared library.  
The problems are caused by lua interpreter unloading module before sanitizers build a report. See [asan issue #89](https://github.com/google/sanitizers/issues/89) for some details.

This recipe prevents module premature unload, thus avoiding false positives and producing correctly resolved backtraces in sanitizers reports.


### Usage:
Add to the `ya.make` of your DLL or LIBRARY(in scheme with DLL_FOR):  
`INCLUDE(${ARCADIA_ROOT}/maps/infra/recipes/luamodule_sanitizer_cure/recipe.inc)`
