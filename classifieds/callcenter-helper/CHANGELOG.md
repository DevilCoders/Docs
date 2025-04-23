## callcenter-helper:1.14.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-254: passport client with tvm

## callcenter-helper:1.13.2 (Mon, 23 Aug 2021 18:59:00 +0300)

 * bump

## callcenter-helper:1.13.1 (Mon, 23 Aug 2021 18:59:00 +0300)

 * bump

## callcenter-helper:1.13.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-247: set user id in seller name in case name is invalid

## callcenter-helper:1.12.2 (Mon, 23 Aug 2021 18:59:00 +0300)

 * bump

## callcenter-helper:1.12.1 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-245: form from draft

## callcenter-helper:1.12.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-244: add context to exception to log with request id

## callcenter-helper:1.11.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-240: generate offer form from parsing by hash, update deps

## callcenter-helper:1.10.5 (Mon, 23 Aug 2021 18:59:00 +0300)

 * additional logging temporarily

## callcenter-helper:1.10.4 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-221: update user draft with checking for free placement

## callcenter-helper:1.10.3 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-210: fix import verba, remove not imported data

## callcenter-helper:1.10.2 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-199: available_steering_wheel
 * VSEXTADAPROC-197: fix tech param filter

## callcenter-helper:1.10.1 (Mon, 23 Aug 2021 18:59:00 +0300)

 * add frame regex

## callcenter-helper:1.10.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-189: frame/vin separation
 * VSEXTADAPROC-190: add years to verba suggest

## callcenter-helper:1.9.2 (Mon, 23 Aug 2021 18:59:00 +0300)

 * bump

## callcenter-helper:1.9.1 (Mon, 23 Aug 2021 18:59:00 +0300)

 * bump

## callcenter-helper:1.9.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-180: fix load verba, use update or create, fix license plate validation, catch passport errors
 * VSEXTADAPROC-184: fix license plate formatting

## callcenter-helper:1.8.3 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-179: fix seller name
 * pass request id to services requests

## callcenter-helper:1.8.2 (Mon, 23 Aug 2021 18:59:00 +0300)

 * log passport requests and invalid results

## callcenter-helper:1.8.1 (Mon, 23 Aug 2021 18:59:00 +0300)

 * bump

## callcenter-helper:1.8.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-174: check placement route

## callcenter-helper:1.7.9 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix draft creation

## callcenter-helper:1.7.8 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix offer creation, cc flag set
 * fix is_free_placement_available check

## callcenter-helper:1.7.7 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix auth dep

## callcenter-helper:1.7.6 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix offer get check

## callcenter-helper:1.7.5 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-170: set source when creating offers to fill source info
 * VSEXTADAPROC-171: fix is_free_placement_available check
 * fix geocoder suggest

## callcenter-helper:1.7.4 (Mon, 23 Aug 2021 18:59:00 +0300)

 * bump to update config

## callcenter-helper:1.7.3 (Mon, 23 Aug 2021 18:59:00 +0300)

 * don't propagate tortoise exceptions to api
 * fix cc set in idm auth

## callcenter-helper:1.7.2 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix origin_url length

## callcenter-helper:1.7.1 (Mon, 23 Aug 2021 18:59:00 +0300)

 * add callcenter and role name to user queryset

## callcenter-helper:1.7.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * VSEXTADAPROC-131: idm auth, login instead of email

## callcenter-helper:1.6.3 (Mon, 23 Aug 2021 18:59:00 +0300)

 * bump

## callcenter-helper:1.6.2 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix client headers
 * search by origin id

## callcenter-helper:1.6.1 (Mon, 23 Aug 2021 18:59:00 +0300)

 * bump

## callcenter-helper:1.6.0 (Mon, 23 Aug 2021 18:59:00 +0300)

 * add indexes to optimise future queries
 * filter avito_id in offer
 * filter offers by federal subject
 * location suggest  with type name
 * import all locations to support foreign key in offer
 * filter offers by phone with contains

## callcenter-helper:1.5.6 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix upload_offers out

## callcenter-helper:1.5.5 (Mon, 23 Aug 2021 18:59:00 +0300)

 * /api prefix

## callcenter-helper:1.5.4 (Mon, 23 Aug 2021 18:59:00 +0300)

 * atomic import verba obj create
 * lint
 * fix import verba for super-gen

## callcenter-helper:1.5.3 (Mon, 23 Aug 2021 18:59:00 +0300)

 * add hash to upload_offers response
 * add description to upload offers fields

## callcenter-helper:1.5.2 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix supervisor log output

## callcenter-helper:1.5.1 (Mon, 23 Aug 2021 18:59:00 +0300)

 * fix logging output

## callcenter-helper:1.5.0 (Thu, 24 Dec 2020 18:52:00 +0300)

 * VSEXTADAPROC-120: json logs

## callcenter-helper:1.4.1 (Thu, 24 Dec 2020 18:52:00 +0300)

 * bump version

## callcenter-helper:1.4.0 (Thu, 24 Dec 2020 18:52:00 +0300)

 * VSEXTADAPROC-107: bulk offers upload route
 * VSEXTADAPROC-102: update deps, refactor, async tests, bunker name in cc

## callcenter-helper:1.3.1 (Thu, 24 Dec 2020 18:52:00 +0300)

 * fix import locations
 * fix post migrations hook

## callcenter-helper:1.3.0 (Thu, 24 Dec 2020 18:52:00 +0300)

 * VSEXTADAPROC-82: prometheus metrics, request id in logs, pydantic settings

## callcenter-helper:1.2.4 (Thu, 24 Dec 2020 18:52:00 +0300)

 * VSEXTADAPROC-81: filter by year for tech params verba suggest
 * fix verba keys parsing

## callcenter-helper:1.2.3 (Thu, 24 Dec 2020 18:52:00 +0300)

 * remove parsing submodule
 * fix imports

## callcenter-helper:1.2.2 (Thu, 24 Dec 2020 18:52:00 +0300)

 * schema-registry package
 * update dependencies

## callcenter-helper:1.2.1 (Thu, 24 Dec 2020 18:52:00 +0300)

 * fix truck and moto fields

## callcenter-helper:1.2.0 (Thu, 24 Dec 2020 18:52:00 +0300)

 * offer id field
 * set call center in source

## callcenter-helper:1.1.3 (Thu, 24 Dec 2020 18:52:00 +0300)

 * fix scheduler

## callcenter-helper:1.1.2 (Thu, 24 Dec 2020 18:52:00 +0300)

 * bump

## callcenter-helper:1.1.1 (Thu, 24 Dec 2020 18:52:00 +0300)

 * scheduler

## callcenter-helper:1.1.0 (Thu, 24 Dec 2020 18:52:00 +0300)

 * VSEXTADAPROC-75: update aerich, new fields, check free placement, fixes

## callcenter-helper:1.0.2 (Thu, 24 Dec 2020 18:52:00 +0300)

 * bump version

## callcenter-helper:1.0.1 (Thu, 24 Dec 2020 18:52:00 +0300)

 * fix verba route, offer save route

## callcenter-helper:1.0.0 (Thu, 24 Dec 2020 18:52:00 +0300)

 * VSEXTADAPROC-68 : download data from verba

## callcenter-helper:0.6.1 (Mon, 29 Jun 2020 18:52:00 +0300)

 * fix keyerror when fetching car form with missing fields

## callcenter-helper:0.6.0 (Mon, 29 Jun 2020 18:52:00 +0300)

 * VSEXTADAPROC-53: generate offer schema using pedantic schema mechanism
 * update submodules

## callcenter-helper:0.5.2 (Mon, 29 Jun 2020 18:52:00 +0300)

 * supervisor stop as group

## callcenter-helper:0.5.1 (Mon, 29 Jun 2020 18:52:00 +0300)

 * format api clients common

## callcenter-helper:0.5.0 (Mon, 29 Jun 2020 18:52:00 +0300)

 * update submodules

## callcenter-helper:0.5.0 (Mon, 29 Jun 2020 18:52:00 +0300)

 * VSEXTADAPROC-53: new schema route, based on pydantic schema generation

## callcenter-helper:0.4.0 (Mon, 29 Jun 2020 18:52:00 +0300)

 * VSEXTADAPROC-52: use offer/send route in parsing to get next offer

## callcenter-helper:0.3.0 (Mon, 29 Jun 2020 18:52:00 +0300)

 * VSEXTADAPROC-49: return verba suggest objects in offer form

## callcenter-helper:0.2.1 (Mon, 29 Jun 2020 18:52:00 +0300)

 * refactored verba api and crud a bit

## callcenter-helper:0.2.0 (Mon, 29 Jun 2020 18:52:00 +0300)

 * show region names in callcenter listing
 * schedule verba import
 * fix deploy script may not determine branch name with non-mac git

## callcenter-helper:0.1.2 (Mon, 29 Jun 2020 18:52:00 +0300)

  * do not log ping requests

## callcenter-helper:0.1.1 (Mon, 29 Jun 2020 18:52:00 +0300)

  * set statement_cache_size to 0 for pgbouncer :C

## callcenter-helper:0.1.0 (Mon, 29 Jun 2020 18:52:00 +0300)

  * VSEXTADAPROC-40: access logging middleware with context

## callcenter-helper:0.0.1 (Mon, 29 Jun 2020 18:52:00 +0300)

  * initial release
