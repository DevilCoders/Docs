Maps Common Library
===================
This library contains utilities common for all maps projects.


Enumeration Bitset (enum_bitset.h)
----------------------------------
A convenience class to use enumerations as flags without converting them to or from the underlying type all over the place. The provided metaclass `EnumBitset` is a wrapper around `std::bitset`, it provides a set of typesafe convenience functions. The typesafety is provided by prohibiting usage of other than the base enumeration types.

The only limitation imposed on the base enumeration class is that it must contain special value `ENUM_BITSET_SIZE` as its last member. Otherwise `EnumBitset` will not be compiled.


### Example

    enum class Color: unsigned char {
        Red,
        Yellow,
        Green,
        EnumBitsetFlagsEnd                                  // Will not be compiled without this value
    };
    using TrafficLight = EnumBitset<Color>;

    bool isRoadOpen(const TrafficLight& trafficLight)
    {
        return
            trafficLight.isSet(Color::Green) ||
            trafficLight == ~TrafficLight(Color::Green);    // Red + Yellow => Green will appear be soon.
    }

    bool isFlashing(const TrafficLight& trafficLight)
    {
        return trafficLight.any();
    }

    void switchToGreen(TrafficLight* trafficLight)
    {
        trafficLight->reset();
        trafficLight->set(Color::Green);
    }
