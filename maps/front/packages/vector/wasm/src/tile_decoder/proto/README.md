Protobuf messages are decoded by protobuf-c (https://github.com/protobuf-c/protobuf-c). C implementation is used 
because of huge output code size of google's C++ implementation.

TODO: Current message files from `@yandex-int/maps-proto-schemas` are compiled manually and committed into repo
because of laziness of the author, their compilation must be integrated into build process.
