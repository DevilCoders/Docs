### Vinyl 
Library to make memory mmaped ready binary databases with user defined types 

#### Supported data types

* binary search tree (TSet, TMap)
* dynamic array (TVector)
* hash table (THashMap)
* linked list (TList), more compact alternative for vector, when no random access is needed
* compact string (TCString), more compact alternative for short strings (size < 256)
* string (TString) - strings (size + array of chars)
* tuple (TTuple) - allows to store any kind of types (supports more than one dynamic fields)
* user defined types (structures), supports packed flat structures (only last member may be dynamic)
* various types of varint

For extending library just specify structures NVinyl::TTypeSpec and NVinyl::TTypeTraits for your own type.

#### Size overheads

| K/T     | TCString | TString | TTuple | THashMap                   | TSet/TMap           |  TVector            | TList |
|:-------:|:--------:|:-------:|:------:|:--------------------------:|:-------------------:|:-------------------:|:------------:|
| Static  | 1        |  4      | 0      | 12 + 4 * BZ + B            | 4                   | 4                   | 8            | 
| Flat    | -        |  -      | 0      | 12 + 8 * BZ + B + P(T) * C | 12 + (8 + P(T)) * C | 12 + (8 + P(T)) * C | 8 + P(T) * C |
| Dynamic | -        |  -      | 8 * C  | 12 + 8 * BZ + B + P(T) * C | 12 + (8 + P(T)) * C | 12 + (8 + P(T)) * C | 8 + P(T) * C |

* T - type of value (for the instance std::pair<K, V> for TMap and THashMap) 
* C - count of items
* B - count of buckets (the next power of 2 higher or equal to `C / 0.7`)
* BZ - compressed number of buckets, it may be equal B >> Z, where Z is window size (0, 1, 2)
* P(T) - padding for T - (sizeof(T) % 4)

#### Example

see tests

Examples of typical usage:  
https://a.yandex-team.ru/review/1630731  
https://a.yandex-team.ru/review/1600891

#### TODOs:

* Benchmarks

#### NOTES:

* You should use TReadOnly mode to mount an existing file because the data structure contents for TReadOnly mode & TReadWrite differ.
* Dynamic sized member of your structure should be aligned by 8 bytes due to internal library restrictions. Otherwise, you can get very tricky run-time errors typically on structure size computation.
