# Releases

To release do
```
npm i
npm publish --registry=http://npm.yandex-team.ru
```


# Howto

## Prerequisites

Stylobate should be included before header.styl (either standalone or via nanoislands)
Passport client-js should be included before header.js
If project uses putils.i18n, it should be configured before header.yate.externals.js is run

Some files should be available in your static build:
./files/tb-regular.ttf in ../fonts/tb-regular.ttf
and images in ../i/<images>

## Setup

Borschik-include
* header.js to your client.js build,
* header.yate to your yate build

Include header.styl to your stylus build via @import directive.
Import yate js externals by running `require('pheader/header.yate.externals.js')(require('yate/lib/runtime.js'))`


## Usage

In yate call the pheader external 

```
pheader({
    'tld': 'com.tr' //String, required. TLD.
    'language': 'ru' //String, required. Two-letter language code.
    'service': 'Service name' //String, optional. 'Паспорт' if undefined
    'serviceUrl': 'http://yandex.ru' //String, optional. Url for the logo link, '/' if undefined
    'username': 'vasya@mail.ru' //String, optional.
    'logoutRetpath': 'http://google.com' //String, optional.
    'authlink': true() //Boolean, optional. Whether to show a link to authorization. False by default.
}, {
    'isTouch': false() //Whether the header is in touch environment
    'hideuser': false() //Set "true" if you want hide user-block
    'env': 'production' //Current environment
    'theme': 'white' //White by default. May be 'black'
})
```
