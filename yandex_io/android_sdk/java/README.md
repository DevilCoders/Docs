You can generate JNI C++ headers from java with gradle task:

./gradlew generateJniHeaders -Pinternals.skip_io_sdk_build=true
-Pinternals.skip_io_sdk_build=true - allows to generate headers even if native io sdk build is broken

Unforturnately kotlin has no builtin jni headers generator https://youtrack.jetbrains.com/issue/KT-35127
So by now android jni classes should be strictly written ONLY IN JAVA.

