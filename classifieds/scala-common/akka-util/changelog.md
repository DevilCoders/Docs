# Change Log
All notable changes to this project will be documented in this file.

File format described [here](http://keepachangelog.com).

## [1.0.7] - 2016-12-14
### Changed
  * AUTO-9309: Added severity setting for event period checks in PeriodicEventHealthCheck

## [0.14.5] - 2016-04-22
### Fixed
  * VSINFR-806: Sync with Zookeeper in PusherExtension
    * Used updated DeployAwareServiceDiscovery from curator-recipes based on Zookeeper map

## [0.14.4] - 2016-03-03
### Fixed
  * VSINFR-934: Regular re-registration in ActorServiceDiscovery
    * Correct ActorSelection construction from ActorRef
    * Use `putIfAbsent()` instead of `put()` for register ActorSelections within `ZooKeeperMap` 
    * More robust ActorServiceDiscoverySpec

## [0.14.3] - 2016-02-10
### Fixed
  * RABOTA-3889: Removed brackets from monitoring messages which was mistakenly recognized
    as HTML tags by monitoring frontend
    
### Added
  * ActorMonitorTest

## [0.14.2] - 2016-02-10
### Fixed
  * VSINFR-896: ActorServiceDiscovery doesn't restore nodes
  * Tests on ActorServiceDiscovery fixed
  * Some cases in PartitionMessageStorageSpec and ConcurrentTotalResourceCounterTest ignored
    (wait VSINFR-882)

## [0.11.0] - 2015-10-14
### Changed  
  * DeployAwareServiceDiscovery moved to curator-recipes
  * ZooKeeperMap moved to curator-recipes
  * curator-recipes used
  * RunWith(JUnitRunner) removed
  * Try to make more robust tests
  

