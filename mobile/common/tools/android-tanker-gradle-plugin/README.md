# android-tanker-plugin
Gradle plugin for strings from tanker

# Before usage
You need own OAuth token to communicate with tanker api.
Obtain token [here](https://nda.ya.ru/3SjQY7).
Then set environment variable `TANKER_API_TOKEN`:
`export TANKER_API_TOKEN=<your token>`.
You can add this line to your `.bash_profile` or `.zshrc` to automatically setup token on login.

# Release
1. Update version in build.gradle
2. Run release build at https://teamcity.yandex-team.ru/buildConfiguration/MobileNew_Monorepo_Common_Tools_AndroidTankerGradlePlugin_Release

# Third party description of this plugin
https://wiki.yandex-team.ru/users/hatter/android-tanker-plugin/
