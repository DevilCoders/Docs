Usage:
In root gradle project's settings.gradle add apply string, and call include function with all subprojects, that required for project:
```
apply from: "<path-to-disk-common-directory>/gradle/settings.gradle"
includeCommonDiskModules('<path-to-disk-common-directory>/modules/', 'logger', 'http-client', ... '<some module name>')
```

If You add new common gradle module, then you must add module name to DISK_COMMON_MODULES map in
```
<path-to-disk-common-directory>/gradle/settings.gradle"
```

Run all tests
```
./gradlew jvmTest
```
