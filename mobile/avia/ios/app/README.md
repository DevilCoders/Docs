# mobile-avia-client-ios

## Set up

```bash
brew install rvm
rvm install 2.2.2
rvm use 2.2.2

gem install bundle
bundle install

pod install
```

## Modify testing endpoint

If you want to modify testing endpoint for developing purposes, first step is changing *webEndpoint* variable in `YaAvia/Managers/YASettingsManager.m`  
Then, if your website can be opened successfully in Safari, but fails in app with SSL errors,
you need to disable [forward secrecy](https://developer.apple.com/documentation/security/preventing_insecure_network_connections)
in `YaAvia/Supporting Files/YaAvia-Info.plist`, by adding this code:

```xml
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSExceptionDomains</key>
    <dict>
        <key>my.very.very.faulty.domain.net</key>
        <dict>
            <key>NSExceptionRequiresForwardSecrecy</key>
            <false/>
        </dict>
    </dict>
</dict>
```

see SUBURBAN-1864
