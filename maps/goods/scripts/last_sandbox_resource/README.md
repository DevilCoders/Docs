# Last Sandbox Resource

This script gets from Sandbox a download URL for the last resource with type GEOSEARCH\_FUNDUK\_PACKAGE for the right staging (stable or testing). It's needed to integrate funduk core CI and Nirvana.

It's intended to be used with [Python3 Processor JSON to JSON](https://nirvana.yandex-team.ru/operation/bc583b47-cd94-4af4-9b87-a545dd07b9fa) operation. It takes a staging as an input parameter from JSON field ``env`` and returns a download URL as an output JSON field ``funduk_resource_url``.
