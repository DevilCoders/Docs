# Library for storing and reading historical track data.
## General
This library provides read and write functionality for storing and accessing historical tracks data.

### Start saving data from geobus in service
You should only add component trackstory::TrackGeobusSaver to you service components and your service will
start saving positions from geobus to Redis. And also set configs for this component.
See documentation for component for configs.
