Some basic checkstyle integration (also, pmd and findbugs could be run, in principle, but they are not configured yet).
At the moment, the `check` gradle task does not depend on the code quality tasks to prevent bloating the Teamcity build
log (with the current config there are _a lot_ of codestyle violations). So, there are two options:

* you can just run `./gradlew checkstyle`
* you can install the [IDEA plugin](https://github.com/jshiell/checkstyle-idea), and run the checks with the same
 config from the IDE, they actually have pretty output. You can also run the checks for the current VCS changeset only.
 Also, configure the SevNTU checks for your IDE: https://github.com/sevntu-checkstyle/sevntu.checkstyle/wiki/How-to-use-SevNTU-Checkstyle-in-Intellij-IDEA.

Both of those quite useless though unless we explicitly fix most of these violations, so it'd really be possible to
 check that someone's commit violated the code style.

Check out the file `config/checkstyle/checkstyle.xml` to see what checks are in use and `config/checkstyle/suppressions.xml` for the suppressions.

There are html reports available, though their names are not printed in the gradle output (TODO most likely, a bug in
the plugin).

However, the html's report filename is the same as xml's (which is being printed), so just change the extension and open
 the link in the browser.