# yandex-taxi-phone-switcher
A simple script for switching group phone number to current on-call engineer.

## Requirements
### Required FW access
* `http://calendar-api.tools.yandex.net` - for retrieving duty calendar
* `https://staff-api.yandex-team.ru` - for retrieving engineer's phone number
* `http://bot.yandex-team.ru` - for switching group number on the engineer's phone

### Calendar requirements
Every calendar event must have on-call egineer's login in the name of the event in the form `username@` (`-` and `_` are accepted as valid symbols). If there's more than one login in the event, the first one is used and other are ignored. The behaviour is undefined if there's more than one event at a given time.

### OAuth token requirements
There are no special requirements for oauth token.

## Usage
Typical parameters are these: `taxi-phone-switcher.py --cal-token <calendar token> --phone <group phone> --oauth <oauth token or file>`.
* `<calendar token>` - is a private token of duty calendar, that is used to determine current on-call engineer
* `<group phone>` - is a phone number, that should be switched to current on-call person
* `<oauth token or file>` - should be either valid OAuth token, or a file with it

There's also couple of debug parameters like `--dry-run` that will do everithing except actual switching, and `--debug` that will show you a bit more output and hopefully help to debug problems.
