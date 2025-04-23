## About

AppRecKit allows you to use Yandex's app recommendations, with complete freedom of implementation for loading and showing recommendations to the end user.

## Setting up the SDK

To use the SDK, add the library to your project manually.

1. Download and unpack the AppRec SDK.

2. Copy the RecKit-core.aar file from the AppRec/lib folder and put it in your project's apps/libs folder. (You will need to create this folder if it does not already exist.)

3. Add the following lines to your app module's build.gradle file:

```java
repositories {
   flatDir {
      dirs ​ 'libs'
   }
}
dependencies {
...
   compile(name: ​ 'RecKit-core'​ , ext: ​ 'aar'​ )
}
```

4. Add the _android.permission.INTERNET_ permission to _AndroidManifest.xml_ for your application:

```xml
<?xml version= "1.0"  encoding= "utf-8" ?>
...
<manifest xmlns:android= "http://schemas.android.com/apk/res/android">

    <uses-permission android:name="android.permission.INTERNET" />

</manifest>
```

## Initialization

Put the initialization code in the onCreate method of the Application or Activity class. The key initialization parameters are _clid_ and _recCount_:

```java
import com.yandex.reckit.core.AppRecKit;
import com.yandex.reckit.core.config.AppRecKitConfig;
...

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        ...
        if (!AppRecKit.isInitialized()) {
            AppRecKitConfig.Builder builder = AppRecKitConfig.newAppBuilder();

            // List of installed packages.
            // false: disable sending (default).
            // true: enable sending.
            builder.setAllowSendPackagesList(true);

            // Required partner ID (clid), which is issued to you by a Yandex manager on request.
            // For testing, use the value 2297779.
            builder.setClid(2297779);

            // Maximum number of recommendations in the loaded list.
            builder.setRecCount(10);

            AppRecKit.initialize(context.getApplicationContext(), builder.build());
        }
    }

```

## Getting data about recommended apps

After proper initialization of the library, you can start loading app recommendations.

1. Implement the logic for processing loaded recommendations:

    ```java
    import com.yandex.reckit.core.service.IAppRecKitItemsProvider;
    ...
    class Callback implements IAppRecKitItemsProvider.ICallback {
    
        @Override
        public void onLoaded(@Nullable IRecItemsPage data, @NonNull RecSource source) {
            if (data == null || data.getItems().isEmpty()) {
                // No data on provided page.
                return;
            }
            for (IRecItem recItem : data.getItems()) {
                // Process loaded recommendations here.
                ...
            }
        }
    
        @Override
        public void onLoadFailed(int pageId, @NonNull RecError error, @Nullable IRecItemsPage oldData) {
            // Error handling.
            ...
        }
    }
    ```

2. Add the code for loading recommendations (note that loading is paginated):

    ```java
    
    import com.yandex.reckit.core.AppRecKit;
    import com.yandex.reckit.core.service.IAppRecKitItemsProvider;
    ...
    
    // Each part of the app that displays recommendations (Activity/Fragment/View)
    // must have a unique identifier (we call it placementId).
    String placementId = "XXX"; // Replace with your identifier (call it activity/fragment or something similar).
    
    // Callback for processing loaded recommendations. 
    Callback callback = new Callback();
    ...
    
    /**
     *
     * @param pageNumber The page number for loading recommendations, starting from 0.
     */
    private void loadRecItems(int pageNumber) {
        IAppRecKitItemsProvider itemsProvider = AppRecKit.getItemsProvider();
        if (itemsProvider != null) {
            itemsProvider.load(placementId, pageNumber, callback, false);
        }
    }
    ```

3. (Optional) It is possible to load recommendations only for specified app categories:

    ```java
    import java.util.EnumSet;
    ...
    // Example: Load only recommendations of apps in the news and entertainment categories.
    EnumSet<RecCategory> recCategories = EnumSet.of(RecCategory.NEWS, RecCategory.ENTERTAINMENT);
    
    itemsProvider.load(placementId, pageNumber, callback, recCategories, false);
    ```

4. To cancel loading of recommendations that has already started (for example, if the app switched to the background), add the following code to onPause/onStop Activity or Fragment:

    ```java
    @Override
    public void onStop() {
        super.onStop();
        IAppRecKitItemsProvider itemsProvider = AppRecKit.getItemsProvider();
        if (itemsProvider != null) {
            itemsProvider.cancel(placementId);
        }
    }
    ```

## Opening app links to Google Play Store

The app link contained in _IRecItem.getDownloadUrl_ can be a tracking link.
To correctly open this type of link in Google Play Store, you must expand it correctly.

For this reason, you should always use InstallHelper to access an app page from recommendations:

```java
import com.yandex.reckit.ui.install;
...
InstallHelper.openApp(context, recItem);
```

## Collecting statistics

AppRecKit supports collecting statistics about app recommendations viewed on the user's screen and sending the statistics to the server.

IMPORTANT: Collecting and sending statistics affects optimization of promo offer displays, so it can also affect revenue.

Use the following code:

```java
IRecItem recItem = <code for getting the recommendations that are shown to the user>

if (AppRecKit.isInitialized()) {
    AppRecKit.getAppStatisticManager().recItemViewed(recItem);
}
```

## Improving quality of recommendations

In order for the recommendations system to work properly, it must receive information about the apps installed on the device.

When you configure AppRecKit, enable sending the list of packages:

```java
AppRecKitConfig.Builder builder = AppRecKitConfig.newBuilder();

// List of installed packages.
// false: disable sending (default).
// true: enable sending.
builder.setAllowSendPackagesList(true);
```

> **Note:**
You must add information to your license agreement stating that you send the list of installed packages to a third party.

### Sending geolocation

To send the geolocation:

1. Declare the permission in your manifest:

    ```xml
    <manifest  xmlns:android= "http://schemas.android.com/apk/res/android">
    ...
    <uses-permission android:name= "android.permission.ACCESS_FINE_LOCATION" />
    ...
    </ manifest>
    ```

2. Request permissions in Activity:

    ```java
    @Override
    public void onCreate() {
        super.onCreate();
        if (AppRecKit.isInitialized()) {
            // Permissions request
            AppRecKit.requestPermissions(this);
        }
    }
    ```

