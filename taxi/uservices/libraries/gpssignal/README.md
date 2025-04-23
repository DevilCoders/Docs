# GPS signal library

This small library provides ::gpssignal::GpsSignal structure and serialization and testing methods. All members of ::gpssignal::GpsSignal
are strongly typed. See documentation for this class for more information.

## Serialization

Serialization to/from any supported format is provided in <gpssignal/serialization/gps_signal.hpp> header.

## Testing

1. ::gpssignal::test::GpsSignalTestPlugin provides method for creating test signals and comparing signals.
2. <gpssignal/test/print_to.hpp> provides PrintTo method to use in Google Tests. All you need is to include that header.
