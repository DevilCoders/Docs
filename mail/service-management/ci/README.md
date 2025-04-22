# ci

## Premise

This is a Python3 utility designed to ease RTEC unified projects build and deployments into QLOUD.

## Requirements

Python3
modules: `pip3 install -r requirements.txt`
[asg](https://bb.yandex-team.ru/projects/MAIL/repos/asg/browse/README.md)

## Syntax and operation

Call `./ci --help` for usage.

## Configuration

1. `global.yml` holds the global configuration (QLOUD urls etc.)
2. `app.yml` holds the app-specific configuration for all the apps

Both files need be present in the same folder as the `ci` script.

## Credentials

### 1. ~/.docker.token
#### File format
```
<token>
```
#### Where to get token
https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1


### 2. ~/.qloud.token
#### File format
```
<token>
```
#### Where to get token
https://oauth.yandex-team.ru/authorize?response_type=token&client_id=072224ad7c864b158601e49b25497eac


### 3. ~/.jenkins.credentials
#### File format
```
<username> <token>
```
#### Where to get
https://common.jenkins.mail.yandex.net/user/your_yandex_login/configure


### 4. ~/.crt.token
#### File format
```
<token>
```
#### Where to get token
https://oauth.yandex-team.ru/authorize?response_type=token&client_id=8b8ba6767850432b93d0442e4a38dcd6
