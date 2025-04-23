# Example Bitbucket Server Plugins

This repository provides the sources for various plugin examples used in the [developer documentation](https://developer.atlassian.com/bitbucket/server/docs/latest)

* [Custom authentication plugin](authentication)
* [Example Repository Hooks](hooks-guide)
* [Example Repository Merge Check](is-admin-merge-check)
* [Decorating pages in Bitbucket Server](plugin-decorators)
* [Enhancing the pull request overview page](pull-request-ui)

 ```
brew install maven
# downgrade git to 2.19.2
brew unlink git && brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/56cb925d3084c7729a86df6063965b7982cea2d2/Formula/git.rb

mvn install -gs settings.xml
mvn bitbucket:run -gs settings.xml -pl build-manager

# provision test data
sh init.sh
```

open http://localhost:7990/bitbucket  
login/password - admin/admin

## Config processing include and exclude rules:
1. Exclude has higher priority.   
Include - `/root/mail/util`, Exclude - `/root/mail/*`, Result - nothing.   
Include - `/root/common/*`, Exclude - `/root/common/doc`, Result - included everything from `/root/common/` except `/root/common/doc`   
2. If there is no include rules all directories of repository are included.   
3. `*` means any number of any symbols, `.` means a real dot.    
 
**The same rules work for branches**

## Teamcity Access
For plugins with teamcity access you need to put a value of token in bitbucket.properties with key plugin.devtools.oauth   
For local bitbucket server put it in build-manager/target/bitbucket/home/shared/bitbucket.properties after mvn install but before run   
You can find the value here - https://yav.yandex-team.ru/secret/sec-01dg0bn681xfsrxhyecgt0bmcj