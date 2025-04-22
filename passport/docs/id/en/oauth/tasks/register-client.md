# Registering an app

The app developer must register the app on the OAuth server in order to receive tokens for Yandex users.

You can register the app on the [New client]{% if lang == "en" %}(https://oauth.yandex.com/client/new){% endif %} page. Only the name and accesses are required for each app, but more information about the app helps the users understand exactly who they are allowing to access their account.

All apps you created can be found in [your apps list]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %}.

## App description {#general}

The name, icon, and set of required access rights are displayed:

- On the [access request page](../concepts/ya-oauth-intro.md).
- On the [list of apps]{% if lang == "en" %}(https://passport.yandex.com/profile/access){% endif %} the user already allowed access to.
- On the [list of your apps]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %}.

## Platforms {#platform}

Settings specific to the platforms your app is running on. For example, the **Callback URI** field becomes available only if the **Web services** option is selected.

### iOS app {#ios}

#|
|| **iOS Appid (Prefix + Bundle id)** | The exact ID of the iOS app, for example, `A1B2C3D4E5.com.domain.application`.

Learn more about iOS app IDs in the [Apple documentation](https://developer.apple.com/library/content/documentation/General/Conceptual/DevPedia-CocoaCore/AppID.html). || 
|| **iOS AppStore URL** | Link to the app in the AppStore. || 
|#

### Android app {#android}

#|
|| **Android package name** | The app package name (the `applicationId` field in the `build.gradle` file of your module). Read more about Android app IDs in [Android documentation](https://developer.android.com/studio/build/application-id.html). ||
|| **Android Google Play URL** | Link to the app in Google Play. || 
|| **SHA256 Fingerprints** | The certificate fingerprint of your app. Learn more about generating a fingerprint in the [Android documentation](https://developer.android.com/training/app-links/verify-site-associations.html#web-assoc). ||
|#

### Web service {#web}

#|
|| **Callback URI** | The URL that the user returns to after granting or denying access to the app (corresponds to the OAuth `redirect_uri` parameter).

You can specify multiple **Callback URIs** (for example, for testing and production environments). When requesting a token, specify the URL in the `redirect_uri` parameter.

To get debug tokens for this app, click **Set URL for development**. The field will be filled with a test URL that allows you to [get debug tokens manually](get-oauth-token.md).

{% if audience == "internal" %}

This is a required parameter if the app receives tokens by requesting the user's permission. When tokens are received using [other methods](../reference/resource-owner-credentials.md), the parameter is not used.

{% endif %} ||
|#


## Accesses {#scope}

To choose permissions for your app, expand the sections and select the required access rights.

Depending on the selected rights, the moderation requirements and token lifetime may differ (displayed in the **App parameters** block at the bottom of the page).

## App parameters {#params}

This block displays restrictions imposed on the apps based on the chosen access rights. For example, for the Yandex.Webmaster API, the token lifetime is limited to 180 days.

