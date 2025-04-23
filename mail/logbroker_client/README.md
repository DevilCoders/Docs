Python Logbroker Client
=======================

Simple synchronous logbroker client implementation

## Getting Started

Use pip package from [Yandex PyPi](https://pypi.yandex-team.ru/repo/default/yandex-community-logbroker-client-py/)

```
yandex-community-logbroker-client-py
```

Usage example can be found in https://github.yandex-team.ru/mail/logbroker-client-common


## TODO
1) Fix DistributedConsumer
2) Fix/add tests

## Build and Deploy

All process described in `Jenkinsfile`. All commits and PR will be tested on Jenkins.
`Dockerfile` with env setup process is required.

### Release

Release process and version based on git tags.
To deploy new release just create semver tag with name `v{major}.{minor}.{patch}` and then launch build for this tag in jenkins.

[All jenkins branches and tags](https://jenkins.testpers.yandex.net/blue/organizations/jenkins/logbroker-community%2Flogbroker-client-py/branches)

## Development

```
virtualenv venv --python=python2.7
. venv/bin/activate
pip install -r requirements/requirements-dev.txt
pytest
```
