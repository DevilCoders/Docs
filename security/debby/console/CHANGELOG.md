# Changelog
Some (but not all) changes to this project will be documented in this file.

## [0.1.2]
### ADD
- Additional optional field for arbitrary values on policies
- Basic PIPELINES
- CH, Mongo, Redis engines
- Mechanism for exceptions in project targets
### FIX
- More retires on db queries
- Retries on ipv6 fetching
### Changed
- Rewrote splunk event generation code

## [0.1.1]
### Changed
- Now scans run only at specifed interval of time time+30seconds
- Hardcoded macro _DEBBY_ALL_IPV6_ not filters non YNETS addresse
### FIX
- Increased stability by retries
- Increased stability by additional exception handles
### REMOVE
- A lot of logs

## [0.1.0]
