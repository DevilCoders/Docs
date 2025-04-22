# gena

Gena is a code generation tool.

  - Create list of events on wiki. [Example for Yandex.Maps](https://wiki.yandex-team.ru/maps/mobile/analytics/metrics/).
  - Make config.
  - Generate source.
  - Magic!


## Get started

Create `Gemfile`:
```ruby
source "http://rubygems.org" 
gem 'gena', git: 'https://stash.desktop.dev.yandex.net/scm/~baksheev/gena.git'
```


Install bundler and gena gem:
```sh
$ gem install bundler
$ bundle
```


## Configuration

Create `gena.yaml`:
```yaml
gena:
  group_name: 'Maps'
  events_file: 'metrics.xls'
  objc:
    working_dir: './'
  java:
    working_dir: './'
    package: ru.yandex.maps.appkit.analytics
  cs:
    working_dir: './'
    namespace: Yandex.Maps.Services.Analytics
```


## Generation
Generate Objective-C:
```sh
$ gena objc
```
Generate Java:
```sh
$ gena java
```
Generate C#:
```sh
$ gena cs
```
