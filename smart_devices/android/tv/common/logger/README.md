## Add Logger to your project

In repositories section:
```groovy
maven { url 'https://artifactory.yandex.net/artifactory/yandex_mobile_releases/' }
```

In dependencies section:
```groovy
implementation "com.yandex.launcher:logger:$logger_version"
```

## Proguard optimisations

To remove logging code in production build you need to use next dependency:
```groovy
implementation "com.yandex.launcher:logger-cutted:$logger_version"
```

This version of library contains proguard rules that remove all logger calls, except _report()_ calls.

Proguard removes methods calls only if optimization is enabled. Please check, that you use the optimizing version of Android proguard rules:

```groovy
proguardFiles getDefaultProguardFile('proguard-android-optimize.txt')
```

#### R8

If you use R8 in your project, please make sure that you have the latest version of R8:

```groovy
repositories {
    ...

    maven {
            url "http://storage.googleapis.com/r8-releases/raw/master"
    }
}

...

ext.r8_version = 1.5.68 // Or later

...

dependencies {
    classpath "com.android.tools:r8:$r8_version" // Must be before the Gradle Plugin for Android.
    classpath "com.android.tools.build:gradle:$gradle_plugin_version"
}
```

Old versions of R8 (< 1.5.68) have issues with code optimization.

## Usage

By default logger prints logs in logcat output and filters secure logs, we are going to discuss how to customize this behaviour in next section.

Tag must be specified each time the logger is called:

```java
Logger.d(TAG, "Log message");
```

#### Secure logs

To avoid disclosing sensitive information, you have to use secure logging:

```java
Logger.secure().i(TAG, "Sensitive information");
```

#### Report errors

To send logs to some external service it is necessary to use _report()_ method:

```java
Logger.report(TAG).e("Error");
```

and implement _ILogFilter_ for _AndroidLogProcessor_ or process _report_ argument in _ILogProcessor_ callback.

#### Throws an exception

Sometimes it is convenient to throw an exception after the error has been logged:

```java
Logger.e("Error", new NullPointerException).throwException();
```

By default, a RuntimeException is thrown, which wraps the original exception. To customize this behaviour you need to implements own _IThrowableHandler_:

```java
public class CustomThrowableHandler implements IThrowableHandler {

    @Override
    public void throwException(@Nullable String msg, @Nullable Throwable tr) {

        //TODO implement logic

    }
}

...

Logger.setThrowableHandler(new CustomThrowableHandler());
```

## Log Processor

If you want to change the log output behaviour, you can implement your own log processor and use it
in the logger:

```java
public class CustomLogProcessor implements ILogProcessor {

    @Override
    public void process(@Priority int priority, boolean secure, @NonNull String tag,
                        @NonNull String fmt, @Nullable Object args, @Nullable Throwable reason,
                        boolean report) {

        //TODO process logs

    }
}

...

Logger.setProcessor(new CustomLogProcessor());
```

There are several predefined processors:

#### AndroidLogProcessor

This processor is used by default in Logger. It prints logs in the default android log output and allows to customize log filtering:

```java
public class CustomLogFilter implements ILogFilter {

    @Override
    public boolean isLoggable(boolean unsafe, @NonNull String tag, int priority) {

        //TODO implement logic for filtering

    }
}

...

Logger.setProcessor(new AndroidLogProcessor(new CustomLogFilter(), null));
```

In addition processor allows to report errors to some external service:

```java
public class CustomErrorReporter implements IErrorReporter {

    @Override
    public void reportError(@NonNull String msg, @Nullable Throwable throwable) {

        //TODO send an error to some service

    }
}

...

Logger.setProcessor(new AndroidLogProcessor(null, new CustomErrorReporter()));
```

#### DumpLogProcessor

Processor stores logs in memory cache and dump them by request. _DumpLogProcessor_ accepts the _ILogFilter_ and _IErrorReporter_ like _AndroidLogProcessor_:

```java
final DumpLogProcessor dumpProcessor = new DumpLogProcessor(new CustomLogFilter(), new CustomErrorReporter());

...

Logger.setProcessor(dumpProcessor);

...

final StringBuilder stringBuilder = new StringBuilder();
dumpProcessor.dump(stringBuilder);
```

It is possible to combine _DumpLogProcessor_ and any other processor:

```java
final AndroidLogProcessor androidProcessor = new AndroidLogProcessor(null, null);
final DumpLogProcessor dumpProcessor = new DumpLogProcessor(androidProcessor);

...

Logger.setProcessor(dumpProcessor);
```
