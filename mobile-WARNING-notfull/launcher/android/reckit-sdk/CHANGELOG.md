Change Log
==========

Version 2.2.0 *(2019-04-12)*
----------------------------
 * move to andoridx
 * split core-impl common things to core-stub and ui

Version 2.1.0 *(2019-04-12)*
----------------------------
 * support v3/recommend api 
 * bugfixes

Version 2.0.0 *(2019-02-22)*
----------------------------

 * Removed embedded metrica and scarabey
 * Refactored flavours
 * Updated Logger
 * Allow set logger via public API
 * Fixed dependencies in .pom files
 * Fixed proguard rules for prod releases

Version 1.1.13-1.1.15 
-----------------------------
 * bugfixes

Version 1.1.12 *(2018-11-08)*
-----------------------------
 * support expire_at configuration
 * bugfixes

Version 1.1.11 *(2018-11-08)*
-----------------------------
 * bugfixes

Version 1.1.10 *(2018-10-26)*
-----------------------------
 * Open disabled/uninstalled apps bonus cards in a proper way
 * Wait give_gifts
 * bugfixes

Version 1.1.9 *(2018-10-26)*
----------------------------
 * Support setting external filters through RecViewConfigInternal
 * Support external recView invalidation
 * Filter out used gifts
 * Refresh recommendations on auth token change
 * Add expired timeout in RecKitItemsLoader

Version 1.1.8 *(2018-10-05)*
----------------------------
 
 * Added AuthTokenProvider
 * Added Cell in LocationProvider
 * Added IClientInfoProvider
 * Added Universal bonus card
 * Reduced methods count with @Thunk annotation
 * Added version in Parcelable objects
 * Removed unused code
 * Corrected proguard rules 
 * Removed non-ascii symbols from user-agent

Version 1.1.7 *(2018-07-16)*
----------------------------

 * Added AppRecKit
 * Extended feedback service 

Version 1.1.6 *(2018-05-22)*
----------------------------

 * Removed LowPriorityHandler and IdleStateController

Version 1.1.5 *(2018-05-18)*
----------------------------

 * Make all resources in library private 
 * Fix proguard rules for ui/core libraries compatibility
 * Bug fixes
 * Add place parameter to rec_feed_open event

Version 1.1.4 *(2018-03-19)*
----------------------------

 * Show disclaimers in zen and fix all disclaimer animation
 * Single screenshot reload

Version 1.1.3 *(2018-02-15)*
----------------------------

 * Small widget UI fixes

Version 1.1.2 *(2018-02-15)*
----------------------------

 * Support scarabey logging
 * Added fontPath attribute, added support Yandex Sans fonts for Zen_Singleapp_card
 * Reduce mem cache for low-end devices, added onTrimMemory() support
 * Added disclaimers and age ratings

Version 1.1.1 *(2018-02-06)*
----------------------------
 
 * Fixed sending of data without accept license agreement
 * Fixed an infinite download of recommendations if an empty list comes in the response
 * Fixed the widget view does not show the error text

Version 1.1.0 *(2018-01-25)*
----------------------------

 * Added stub lib for core
 * Timeout for receiving uuid was added
 * Cards with recommendations are opened in the popup window. IHostView is deprecated
 * Added the ability to apply SDK UI configuration manually
 * Added 'accept license agreement' property  
 * Fixed infinite loading on unstable Internet
 * Fixed missing stubs in the feed
 
Version 1.0.1 *(2017-12-21)*
----------------------------

 * Fix: network data is not sent in LBS info

Version 1.0.0 *(2017-12-18)*
----------------------------

Initial release
