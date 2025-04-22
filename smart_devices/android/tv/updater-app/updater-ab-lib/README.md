# Goal
This library just to allow to compile the project, due to system classes `android.os.UpdateEngine` and `android.osUpdateEngineCallback` can't be accessed at compile time

* These should not be modified somehow, or translated to Kotlin<br/>
* No need to add any code improvements like `IntDef` / `StringDef` etc.<br/>
* No need to check the codestyle for these classes<br/>
* Theses classes must not be obfuscated<br/>
* These classes needed to be up-to-date with platform implementation, so, when updating api level, it is important to check that these classes not changed in new platform
