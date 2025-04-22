Changelog
---------
#### 4.2.1 -- Improve jar archives
* better api for AGP 4.0.+;
* fix java.lang.NoClassDefFoundError: Failed resolution of: Landroidx/appcompat/R$drawable;

#### 4.2.0 -- Support AGP 4.0.+
* this release supports agp 4.0.+ but earlier versions not;

#### 4.1.0 -- Support AGP 3.6.+
* this release supports agp 3.6.+ but earlier versions not;

#### 4.0.1 -- Fix synchronous run
* fixed async running of ajc (which is not supporting async compiling);

#### 4.0.0 -- Support AGP 3.5.+
* this release supports agp 3.5.+ but earlier versions not;

#### 3.4.5 -- Fix for Gradle 6.0
* create task explicitly instead of `project.task()`;

#### 3.4.3 -- Once more fix :(
* hotfixed provides plugin mode — transformation should not starts;

#### 3.4.2 -- Hotfix provides
* hotfixed provides plugin mode — transformation should not starts;

#### 3.4.1 -- Fix provides
* fixed aspectj-provides plugin mode — do not cleanup destination dir;

#### 3.4.0 -- Better DryRun mode
* fixed support of 3.5.0 Android Gradle Plugin — thanks to @superafroman;
* remove aj runtime check;
* standalone DryRun plugin mode to avoid transformation and compilation steps;

#### 3.3.12 -- Fix 'Dependencies resolution fail'
* fixed rare bug — 'failed to attach configuration after dependencies has been resolved';
* better properties extraction within kts script;

#### 3.3.11 -- Fix legacy AGP support
* better legacy support — fixed AGP 3.1.4 compatibility;

#### 3.3.10 -- Update AJC
* bump aspectj compiler version;

#### 3.3.9 -- Small fix dryRun
* to prevent aj transformation with empty outputs — use `-PdryRunAjc=true`;

#### 3.3.8 -- Fix unitTest variant
* added workaround to disable unitTest aj compile step if classpath is broken;

#### 3.3.7 -- Fixes ext plugin
* fixed `aspectj-ext` plugin to work properly with transform api;
* added transform output dir to inPath;
* fix ajc inPath for compilation step;

#### 3.3.6 -- Fixes
* fix dryRun option for transformer;
* better readme;

#### 3.3.5 -- Dry run
* fix classpath resolving;
* implement dry run to disable compiler/transformation in gradle;

#### 3.3.3 -- Support AGP 3.3.+
* fixed support AGP 3.3.+ api;
* added legacy compatibility fallbacks;
* added java bytecode target version for ajc;
* upgrade bundled ajc runtime and tools jars to 1.9.2;
* upgrade default aspectj runtime library to 1.9.2;

#### 3.3.0 -- JUnit tests support
* implementing `com.archinamon.aspectj-junit` plugin supporting weaving unit tests;
* `com.archinamon.aspectj-test` has been removed as not working legacy sh$t;
* updated android-gradle-plugin to 3.2.0 inside (might be a breaking change);
* migration to Kotlin-DSL;
* new plugin tests allows to check does it weaves android's junit source code;

#### 3.2.0 -- Gradle 3.0.0 support
* added support of stable gradle plugin 3.0.0;
* updated internal ajc and provided aj runtime library versions to the latest 1.8.12;

#### 3.1.1 -- Useful improvements
* added an extension trigger to append BuildTime logger for current module;
* back from grave — added exclude-filter for `aspectj-ext` plugin;

#### 3.1.0 -- Provider
* implemented `provides` plugin split to effectively extract aspects to external/sub modules;
* small code improvements and cleanups;

#### 3.0.3 -- Minor fixes
* fixed aar detecting mechanism;
* registered plugin in mavenCentral!

#### 3.0.0 -- Grand refactoring in Kotlin
* all groovy classes was obsolete;
* new code-base in Kotlin 1.1.1 stable;

#### 2.4.3 -- Hot-fixed  two-step compilation
* compiled in first step aspect classes have not been copied to final output;

#### 2.4.2 -- Hot-fix
* fixed missed variable;
* fixed imports;

#### 2.4.0 -- Added aspectj-ext plugin
* `includeJar` parameter now able to read aar's manifest file to exactly detect required library;
* `com.archinamon.aspectj-ext` plugin added to properly weave inpath jars, in this mode InstantRun doesn't allowed;
* small fixes and package/name refactoring;

#### 2.3.1 -- New two-step build mechanic
* renamed extension parameter: ajcExtraArgs -> ajcArgs;
* split parameter: logFileName -> [transformLogFile, compilationLogFile];
* added separate compile task to build all sources under `/aspectj` folder;
* aj-transformer now looks into `/build/aspectj/$variantName` folder for aspects class';
* updated ajc-version to 1.8.10;
* fixed issue with missing error printing to Messages when failing;
* added inpath/aspectpath clearance before emitting transform inputs (by @philippkumar);

#### 2.3.0 -- Major fixes
* InstantRun support;
* fails androidTest hot launch;
* ZipException within augmenting third party libraries via AspectJ;
* more clear logging and errors emitting;

#### 2.2.2 -- Improvements
* fixed build config namings;
* re-designed work with log file and errors handling;
* pretty formatting ajc arguments for build stdout;
* implemented handling custom ajc arguments via build.gradle config;

#### 2.2.1 -- Hot-fix
* fixed illegal 'return' statement;
* change included in `updated` 2.2.0 artifacts;

#### 2.2.0 -- Ajc fixes and improvements
* fixed problem with -aspectPath building project with multidex;
* fixed scope problems with Transform API;
* removed Java 8 support;
* implemented clear and easy way to attach compiled aspects via jar/aar;
* implemented more easy way to weave by aspects any library (jar/aar);
* implemented breaking build on errors occurring to prevent runtime issues;
* implemented ajc experimental features: -XhasMember and -Xjoinpoints:synchronization,arrayconstruction;
* implemented more logic way to detect the plugin placement in build file to support retrolambda correctly;
* code cleanups and improvements;

#### 2.1.0 -- Transform api fix
* finally fixed errors with multidex;
* fixed jar merge errors;
* fixed errors with new gradle plugin;
* fixed Java 8 support;
* fixed Retrolambda compatibility;

#### 2.0.4 -- Small fix
* fixed error with mandatory default aj-directory;

#### 2.0.3 -- Gradle instant run
* merged pull request with the latest gradle plugin update;
* fixed errors after update;

#### 2.0.2 -- Fixed filters
* problem with empty filters now fixed;

#### 2.0.1 -- Hotfix :)
* proper scan of productFlavors and buildTypes folders for aj source sets;
* more complex selecting aj sources to compile;
* more precise work with jars;
* changed jar filter policy;
* optimized weave flags;

#### 2.0.0 -- Brand new mechanics
* full refactor on Transform API;
* added new options to aspectj-extension;

#### 1.3.3 -- Rt qualifier
* added external runtime version qualifier;

#### 1.3.2 -- One more fix
* now correctly sets destinationDir;

#### 1.3.1 -- Hot-fixes
* changed module name from `AspectJ-gradle` to `android-gradle-aspectj`;
* fixed couple of problems with test flavours processing;
* added experimental option: `weaveTests`;
* added finally post-compile processing for tests;

#### 1.3.0 -- Merging binary processing and tests
* enables binary processing for test flavours;
* properly aspectpath and after-compile source processing for test flavours;
* corresponding sources processing between application modules;

#### 1.2.1 -- Hot-fix of Gradle DSL
* removed unnecessary parameters from aspectj-extension class;
* fixed gradle dsl-model;

#### 1.2.0 -- Binary weaving
* plugin now supports processing .class files;
* supporting jvm languages — Kotlin, Groovy, Scala;
* updated internal aj-tools and aj runtime to the newest 1.8.9;

#### 1.1.4 -- Experimenting with binary weaving
* implementing processing aars/jars;
* added excluding of aj-source folders to avoid aspects re-compiling;

#### 1.1.2 -- Gradle Instant-run
* now supports gradle-2.0.0-beta plugin and friendly with slicer task;
* fixed errors within collecting source folders;
* fixed mixing buildTypes source sets;

#### 1.1.1 -- Updating kernel
* AspectJ-runtime module has been updated to the newest 1.8.8 version;
* fixed plugin test;

#### 1.1.0 -- Refactoring
* includes all previous progress;
* updated aspectjtools and aspectjrt to 1.8.7 version;
* now has extension configuration;
* all logging moved to the separate file in `app/build/ajc_details.log`;
* logging, log file name, error ignoring now could be tuned within the extension;
* more complex and correct way to detect and inject source sets for flavors, buildTypes, etc;

#### 1.0.17 -- Cleanup
* !!IMPORTANT!! now correctly supports automatically indexing and attaching aspectj sources within any buildTypes and flavors;
* workspace code refactored;
* removed unnecessary logging calls;
* optimized ajc logging to provide more info about ongoing compilation;

#### 1.0.16 -- New plugin routes
* migrating from corp to personal routes within plugin name, classpath;

#### 1.0.15 -- Full flavor support
* added full support of build variants within flavors and dimensions;
* added custom source root folder -- e.g. `src/main/aspectj/path.to.package.Aspect.aj`;

#### 1.0.9 -- Basic flavors support
* added basic support of additional build variants and flavors;
* trying to add incremental build //was removed due to current implementation of ajc-task;

#### 1.0 -- Initial release
* configured properly compile-order for gradle-Retrolambda plugin;
* added roots for preprocessing generated files (needed to support Dagger, etc.);
* added MultiDex support;