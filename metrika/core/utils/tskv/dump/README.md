dump-tskv
=============

This utility may be used for debug purposes - to dump contents of file in eventlog/protoseq format into tskv.
The escaping of arrays is not standard, so they are treated as usual TSKV strings.

**To enable introspection of your custom eventlog format you need to add descriptor.ev to SRCS() in ya.make**

See `--help` for usage details.
