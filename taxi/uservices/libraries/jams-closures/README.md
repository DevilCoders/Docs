# Library for working with jams and closures
## General
This library provides two main components: ::graph::components::JamsCache and ::graph::components::ClosuresCache and default configuration for them. Both components are registered automatically.

## Usage
To account for jams and closures in your searches on graph, please pass pointers to ::graph::Jams and ::graph::Closures objects into ::graph::DijkstraObjectSearcher constructor. Respective pointers can be obtained from ::jams_closures::components::JamsCache and ::jams_closures::components::ClosuresCache.
Beside those two components, you need actual data files for jams and closures. Those files are downloaded by tool named 'jams-downloader'. See section below for more information about it. If files are not present in system, empty jams and empty closures are provided. Those have no effect on search whatsoever.

!!WARNING!!: Cache components return std::shared_ptr and ::graph::DijkstraObjectSearcher
takes raw pointer .User is responsible that lifetime of ::graph::Jams
and ::graph::Closures objects is greater than ::graph::DijkstraObjectSearcher object.


### Jams-downloader
jams-downloader tool is responsible for downloading jams and closures files to the system. Those files in turn, are used by
::jams_closures::components::JamsCache & ::jams_closures::components::ClosuresCache caches.
To enable jams-downloader tool please follow this manual: https://wiki.yandex-team.ru/taxi/backend/graph/manuals/jamsprepare/ .

## Example
For demo example you can see search_on_graph_test.cpp
