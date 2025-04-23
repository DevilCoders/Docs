1. `ya make -r --maven-export -DJDK_VERSION=8`
2. rename jar and pom with revision suffix from `arc info` like `mv snooper-java.jar snooper-java-8945726.jar; mv pom.xml snooper-java-8945726.pom`
3. upload to https://artifactory.yandex.net/ with target path `ru/yandex/security/snooper-java/8945726`

reference: https://a.yandex-team.ru/arc_vcs/library/java/tvmauth/build_release.md
