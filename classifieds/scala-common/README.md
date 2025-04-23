Repository of more or less common reusable libraries.

### Publish artifacts

CI [build](https://a.yandex-team.ru/projects/verticals/ci/releases/timeline?dir=classifieds%2Fscala-common&id=deploy). Resulting version is 2.0.<release_number>

To publish local snapshot just run ``sbt +publish``.
Know issue here: if you have uncommited changes version would contain timestamp part and it would differ for each scala version  

