## About

RecKit allows you to use Yandex discovery features in your application to show users
personalized app recommendations.

## Add RecKit to your project

In repositories section:
```groovy
maven { url 'http://artifactory.yandex.net/artifactory/yandex_mobile_releases/' }
```

In dependencies section:
```groovy
compile 'com.yandex.reckit:core:1.1.5'
compile 'com.yandex.reckit:ui:1.1.5'

implementation 'com.android.support:recyclerview-v7:27.1.0'
```

Internal version:

```groovy
compile 'com.yandex.reckit:core-internal:1.1.5'
compile 'com.yandex.reckit:ui-internal:1.1.5'

implementation 'com.android.support:recyclerview-v7:27.1.0'
```

## Integration

Depending on your needs you can use RecKit to either show recommendation feed or a single 
recommendation card. To show recommendation feed use class: 

```java
com.yandex.reckit.ui.view.FeedView
```

For single recommendation card use: 

```java
com.yandex.reckit.ui.AppRecView 
```

All classes implement _com.yandex.reckit.ui.IRecView_ interface and are alike to work with.

The following library setup is based on recommendation feed and is relevant for other 
recommendations views.

1. Add _android.permission.INTERNET_ permission into the _AndroidManifest.xml_ of your application:

    ```xml
    <?xml version= "1.0"  encoding= "utf-8" ?>
    ...
    <manifest xmlns:android= "http://schemas.android.com/apk/res/android">
                 
        <uses-permission android:name="android.permission.INTERNET" />
                 
    </manifest>
    ```

2. Insert the following code into the layout of your activity:

    ```xml
    <?xml version= "1.0"  encoding= "utf-8" ?>
    ...
    <FrameLayout xmlns:android= "http://schemas.android.com/apk/res/android"
                 android:id= "@+id/content_view" 
                 android:layout_width= "match_parent" 
                 android:layout_height= "match_parent" >
                 
        <com.yandex.reckit.ui.view.FeedView 
                android:id= "@+id/feed_view"
                android:layout_width= "match_parent"
                android:layout_height= "match_parent" />
                 
    </FrameLayout>
    ```

3. To import RecKit SDK, add the following lines at the beginning of your activity class code:

    ```java
    import  com.yandex.reckit.core.RecKit; 
    import  com.yandex.reckit.ui.view.FeedView;
    ```

4. Declare FeedView variable in the activity class:

    ```java
    FeedView feedView;
    ```

5. You need to configure RecKit before initializing it. Use  RecKitConfig.Builder
   class to specify configuration options:
   
    ```java
    import  com.yandex.reckit.core.config.RecKitConfig;
    
    RecKitConfig.Builder builder = RecKitConfig.newBuilder();
    
    // Mandatory partner id (clid), which can be requested from your Yandex account manager. 
    // For testing use 2297779 
    builder.setClid( "2297779" );
    ```

6. After RecKit is initialized you need to configure its recommendation view. 
   Use _RecViewConfig.Builder_ class for configuration:
   
    ```java
    import  com.yandex.reckit.ui.RecViewConfig;
    
    // Builder receives a mandatory parameter - placement id
    
    // placement id is created by the developer and is needed to distinguish different 
    // recommendation placements
    
    RecViewConfig.Builder viewConfigBuilder = RecViewConfig.newBuilder( "main_view" );
    
    //Optionally a list of app categories to be recommended at a particular placement can be set
    //By default all app categories are recommended 
    
    viewConfigBuilder.addRecCategory(RecCategory.EDUCATION); 
    viewConfigBuilder.addRecCategory(RecCategory.FINANCE);
    ```
    
7. Initialize RecKit and recommendation view in onCreate() method of the Activity:

    ```java
    @override
    public void onCreate() {  
        super .onCreate();
        
        // Initialization of RecKit RecKit.initialize(getApplicationContext(), builder.build());
        setContentView(R.layout.activity_main);
        feedView = (FeedView) findViewById(R.id.feed_view);
        
        // Initialization of recommendation view
        feedView.init(viewConfigBuilder.build()); }
    ```

8. Call recommendation view’s lifecycle methods:
    * _startSession()_ - beginning of user’s interaction with recommendation feed
    * _stopSession()_ - end of user’s interaction with recommendation feed
    * _onShow()_ - recommendation view started being displayed on the screen
    * _onHide()_ - recommendation view stopped being displayed on the screen
    
    App rotation happens outside of user’s interaction with recommendation view (between 
    startSession() and stopSession() lifecycle methods). onShow() and onHide() methods let you 
    account for time during which user sees recommendations, gather stats and rotate recommendations.  
    onShow() and onHide() can be called several times during session.
    
    _processBackButton()_ - handling of “Back” button. Lets you hide expanded cards. _onStart()_, 
    _onStop()_, _onResume()_ and _onPause()_ - are the most suitable Activity methods to call 
    _startSession()_ , _stopSession()_, _onShow()_ and _onHide()_:

    ```java
    @Override
    protected void onStart() {
        super.onStart();
        feedView.startSession(); 
    }
    
    protected void onResume() { 
        super.onResume(); 
        feedView.onShow();
    }
    
    protected void onPause() { 
        feedView.onHide(); 
        super.onPause();
    }
    
    @Override
    protected void onStop() {
        feedView.stopSession();
        super.onStop(); 
    }
    ```

    Handling of “Back” button:

    ```java
    @Override
    public void onBackPressed() {
        if (!feedView.processBackButton()) { 
            super.onBackPressed();
        } 
    }
    ```

9. When recommendation view is no longer needed, you should free up the resources:

    ```java
    @Override
    protected void onDestroy() {  
        if (isFinishing()) {
            feedView.destroy(); 
        }
        super .onDestroy(); 
    }
    ```

## Improving recommendations’ quality

To significantly improve recommendations’ quality RecKit needs the information about apps installed 
on the device, as well as user’s geolocation.

### Sending a list of installed apps

To send a list of installed apps you need to enable this setting when configuring RecKit:

```java
RecKitConfig.Builder builder = RecKitConfig.newBuilder();

// list of installed packages
// false - disable sending (default value) 
// true - enable sending 
builder.setAllowSendPackagesList(true);
```

> **Attention:**
>    To send a list of installed packages you need to include this information into your 
>    application’s License Agreement.

### Sending geolocation

To send the geolocation you need to:

1. Declare the permission in your manifest

    ```xml
    < manifest  xmlns:android= "http://schemas.android.com/apk/res/android" > 
    ...
    < uses-permission android:name= "android.permission.ACCESS_FINE_LOCATION" />
    ... 
    </ manifest >
    ```

2. Ask for a permission in the Activity:

    ```xml
    @override
    public   void  onCreate() {  
        super .onCreate();
        //  Initialization of RecKit
        RecKit.initialize(getApplicationContext(), builder.build());
        // Permissions request
        RecKit.requestPermissions(this); 
    }
    ```
