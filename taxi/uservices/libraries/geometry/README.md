# Geometric Primitives & Algorithms
Library for geographic coordinate system geometry: latitude, longitude, gps signals, and functions for working with them.
All members are in SI and strongly typed to prevent accidental errors.

#### Basic units
The underlying library is Boost::Units and we import many definitions from
there, for example ::geometry::Distance to express distance between positions,
or length of a car, ::geometry::Radians and ::geometry::Degrees to express
plane angle in radians and degrees.

Our ::geometry::Latitude and ::geometry::Longitude are build on a same principle
and support inherent conversion to ::geometry::Degrees for the purposes of
arithmetics. You can do things like that:
```cpp
// if you want to pretend that geographical coordinate system is cartesian
// and need a relation between sides of your bounding box
auto res = 1.0 / (lon1 - lon2) * (lat 1 - lat2)
// or to calculate a perimeter
auto x  = (lon1 - lon2) + (lat1 - lat2)
```

There are additionaly types ::geometry::LongitudeDelta and
::geometry::LatitudeDelta. The purpose of those types is NOT to be used in
arithmetic, but rather to reduce errors in function declarations.
```cpp
void f(LatitudeDelta d_latitude, LongitudeDelta d_longitude);

// The following code will not compile
f(lon1 - lon2, lat1 - lat2);
// To be fare, the following won't compile either:
f(lat1- lat2, lon1 - lon2);
// This is because lat1 - lat2 is NOT a LatitudeDelta. It is a plain degree.
// This one will work:
f( (lon1 - lon2) * dlon, (lat1 - lat2) * dlat);
// The hope is that manually specifying  dlon, dlat will make one more
// attentive.

// However, if you don't wont to mess with Latitude/Longitude Delta, just
// declare function like this:
void y(Degrees d_latitude, Degrees d_longitude);
```

#### Position 
Structure for representing strongly-typed geographic position on the Earth surface.
Position can be created with following expressions:

0. Let x, y, z be double
1. ```Position( x \* ::geometry::lat, y \* ::geometry::lon)```
2. or in different arguments order ```Position( y \* ::geometry::lon, x \* ::geometry::lat)```. Order of arguments is irrelevant.
3. ```Position pos; pos.latitude = x \* ::geometry::lat; pos.longitude = y \* ::geometry::lon;```
4. Less convinient, but still allowed: ```Position pos. pos.latitude = ::geometry::Latitude::from_value(x);  pos.longitude = ::geometry::Longitude::from_value(y);```
5. ```using ::geometry::lon; using ::geometry::lat;``` in method body will make it even more convinient: ```Position{y * lon, x * lat}```

To convert to latitude/longitude to double, use .value() method:

```cpp
double x = pos.latitude.value();
double y = pos.longitude.value();
```

See ::geometry::Position for more detailed information.

#### CartesianPosition
Structure, derived from Position without any overriding, but registered in boost::geometry as cartesian point. Needed for some boost algorithms, such as boost::geometry::intersection 

#### Serialization from/to JSON/BSON/Yaml ####
Methods for serialization from/to JSON/BSON/Yaml are provided in position_serialization.hpp

```
#include <geometry/position.hpp>
#include <geometry/position_serialization.hpp>

::geometry::Position myFunction(const formats::json::Value& value) {
  return value.As<::geometry::Position>();
}

formats::json::Value anotherFunction(const ::geometry::Position& position) {
  return formats::json::ValueBuilder(position).ExtractValue();
}
```

#### BoundingBox
::geometry::BoundingBox is an RFC7945 conformant implementation of BoundingBox,
with support for serialization, operations and other nice things.


#### Distance and Azimuth ####
Function for calculating distance between positions and azimuth between them are in headers distance.hpp and azimuth.hpp

#### Printing ####
units types ( Latitude, Longitude, Distance etc) support printing out of the box. Please include <boost/units/io.hpp>.

#### Testing ####
There are several helper classes and methods in include/test/geometry headers.

1. GeometryTestPlugin - inherit this class in your own test fixture to get access to comparing latitude/longitude, positions and so on.
2. TEST_ macroses from Google test will  print units as expected out of the box
