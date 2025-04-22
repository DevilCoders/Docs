mobile-yandex-mail-ios
======================

Mail address for Yandex Mobile Mail for iOS

# Setup project

To build the project right from the sources of freshly cloned repo, the following steps must be completed:

Install and prepare RVM and Ruby:

- Install RVM (see [RVM homepage](https://rvm.io))
- Install ruby via RVM. Current ruby version is `2.6.5` (see [ruby-version file](./YandexMobileMail/.ruby-version)): `rvm install ruby-2.6.5`
  - For Apple Silicon users: `export optflags="-Wno-error=implicit-function-declaration"; rvm install 2.6.5 --disable-dtrace`
- RVM automatically set environment to ruby version and gemset (yandex-mobile-mail-ios). If not, say `rvm use .` in directory where [.ruby-version](./YandexMobileMail/.ruby-version) and [.ruby-gemset](./YandexMobileMail/.ruby-gemset) files are located
- Check environment: `rvm gemset list`.
- Install `Bundler` gem into current gemset: `gem install bundler -N`
- Update bundle: `bundle update`
- Install all gems from Gemfile: `bundle install`

Prepare project:

1. Install `XCode 13.2.1` or `XCode 13.3` from AppStore.
2. `cd mobile/mail/ios/mail-app/YandexMobileMail`
3. `pod install --verbose`
4. Open workspace in XCode: `YandexMobileMail.xcworkspace`
5. For running on the device (not simulator), log in into developer account and download provision profiles

# Commit rules
1. make sure that there is ticket in StarTrek like 'MOBILEMAIL-XXXXX'. If not - create the ticket.
2. https://wiki.yandex-team.ru/users/turaevt/MergeRulesInMonorepo/

# Wiki
https://wiki.yandex-team.ru/pochta/mobmailios/
