Note that the special "robolectric" flavor should be used for running unit tests.
Hence, you should run unit tests within the "robolectric" flavor whether you are doing that from
terminal (`./gradlew testRobolectricDebug`) or from Android Studio (pay attention to the Build
 Variants tab).

## Running from Android Studio
As for Android Studio 1.2, unit testing is (officially supported)[http://tools.android.com/tech-docs/unit-testing-support]
, and is hardly different from ordinary Junit tests.

## Running from terminal (as Gradle task)
    ./gradlew testRobolectricDebug
The path of the test report will be printed out after the tests execution. Note that in case of
successful tests completion, nothing will be printed.

For more information, please read [wiki](https://wiki.yandex-team.ru/users/karlicos/mailapp-robolectric/).