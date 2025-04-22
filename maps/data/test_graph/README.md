# package yandex-maps-test-graph4

## Description

This package contains test-graph4 files.
These files have already been uploaded to Sandbox and are available in Arcadia at maps/data/test/graph4.

Makefile describes process how graph files are generated.

Tools located here are somehow obsolete but left for historical reasons.

Building graph files process is now broken because YT tables are used to gather information but here Postgres tables are used.

Please do not worry about Makefile dependencies. Now they are already broken because of below removed packages:
* yandex-maps-graph-build-tools2
* yandex-maps-jams-static-graph-tools2
* yandex-maps-turn-penalties
