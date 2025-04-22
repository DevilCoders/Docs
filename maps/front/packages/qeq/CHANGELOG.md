# Changelog

## 1.2.0

### New features

* Added `mute` and `unmute` commands.
* Added `its` command.

## 0.0.9

### Bug fixes

* Fixed `package-lock.json`.

## 0.0.8

### New features

* Added `--log` (`-L`) global option for write logs to file.

### Bug fixes

* Fixed filtering of instances.
* Change texts for overall drills.

## 0.0.7

### New features

* Added confirmation of email notifications in `drill` command ([#11](https://github.yandex-team.ru/maps/qeq/pull/11)).

## 0.0.6

### New features

* Added shell completion via [`tabtab`](https://github.com/mklabs/tabtab) ([#10](https://github.yandex-team.ru/maps/qeq/pull/10)).

## 0.0.5

### New features

* Allowed to specify instance name in `exec` command.
* Now `up` (`down`) command count started (stopped) nodejs process as success execution.
* Added confirmation of issue and event.

### Bug fixes

* Fixed command `exec` with flag `--all`.
* Fixed end date for LSR issue.

## 0.0.4

### Breaking changes

* Changed signature of `exec` command: `qeq exec|up|down <objectId>`.

### New features

* Added command `drill` ([#6](https://github.yandex-team.ru/maps/qeq/pull/6), [#7](https://github.yandex-team.ru/maps/qeq/pull/7)).
* Added command `lsr` ([#8](https://github.yandex-team.ru/maps/qeq/pull/8)).

### Bug fixes

* Fixed error if `ssh` has `stderr`.

## 0.0.3

### New features

* Added command `exec` ([#4](https://github.yandex-team.ru/maps/qeq/pull/4))
* Added parallel ssh to continuously connections ([#3](https://github.yandex-team.ru/maps/qeq/pull/3))
* Added documentation ([#2](https://github.yandex-team.ru/maps/qeq/pull/2))

## 0.0.2

### Bug fixes

* Fixed wildcard for environments ([12e9df2d](https://github.yandex-team.ru/maps/qeq/commit/12e9df2d21bc93c93b08fa502ab3dc234f13bfd3))

## 0.0.1

### New features

* Added commands `up` and `down` ([#1](https://github.yandex-team.ru/maps/qeq/pull/1))
