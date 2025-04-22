# [Yandex Mobile Ads iOS SDK](https://wiki.yandex-team.ru/yandexmobile/appmetrica/ads/sdk/integration/iOS/)

wiki:
https://wiki.yandex-team.ru/yandexmobile/appmetrica/ads/sdk/

Bugtracker:
https://st.yandex-team.ru/ADLIB

TeamCity:
https://teamcity.yandex-team.ru/project.html?projectId=MobileAdsLibrary_MobileAdsLibraryIos&tab=projectOverview

## Сборка проекта

Для сборки проекта необходима ОС MacOS.

1. Установить Xcode. Рекомендуем установить версию из AppStore.
1. Проверить версию ruby, выполнив команду ```ruby -v```. Должна использоваться версия ```ruby 2.6.5```. Иначе нужно установить нужную версию ruby. Для этого нужно установить rvm, согласно [инструкции](https://rvm.io/rvm/install). Для этого нужно:
    1. Установить GPG ключи командой ```gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB```
    1. Установить rvm командой ```\curl -sSL https://get.rvm.io | bash -s stable```
    1. Установить ruby командой ```rvm install ruby-2.6.5```
    1. Выбрать версию ruby 2.4.0 для использования командой ```rvm use 2.6.5```
1. Склонировать [репозиторий с тестовым примером](https://bitbucket.browser.yandex-team.ru/projects/ML/repos/mobile-ads-library-ios/browse).
1. Установить bundler командой ```gem install bundler``` . С полной инструкцией по работе с bundler можно ознакомиться [тут](https://bundler.io).
1. Перейти в корень репозитория в терминале и запустить команду ```bundle install```.
1. Убедиться, что установлена система управления зависимостями [cocoapods](https://cocoapods.org). Для этого нужно выполнить команду ```bundle exec pod --version```. Результат выполнения не должен быть пустым. В случае, если cocoapods не установлены, нужно выполнить команду ```sudo gem install cocoapods```.
1. Запустить в терминале команду ```bundle exec pod install```.
1. Открыть ```YandexMobileAds.xcworkspace``` в Xcode.
1. Выбрать схему  ```AdsSample```, выбрать симулятор и нажать Run.
![project](https://jing.yandex-team.ru/files/xardas/2018-03-06_16-37-18.png)

