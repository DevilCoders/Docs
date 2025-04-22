## [Solomon admin UI](https://solomon.yandex-team.ru/admin)

### Installation

1. Install Node.js: https://nodejs.org/en/ (12.18.4 version recommended, but it can work in the newest versions)
2. Install Yarn package: https://yarnpkg.com/en/docs/install
3. Get necessary dependencies:
```bash
$ make get-deps
```

### Development

Run dev server and open ```localhost:3000``` in browser
```bash
$ make run-web
```

Also you can create "React App" project from existing source in Webstorm and start to develop.

To run with prestable gateway:
1. Change `proxy` property in `package.json` to `http://solomon-prestable.yandex.net`
2. Change `return { Authorization: ``AsUser ${Auth.state.login()}`` };` in `src/api/http.js` to `return { Authorization: 'OAuth AQAD-xxxxxx' };`
3. Restart dev server

```
andreyst-osx:web andreyst$ pwd
/Users/andreyst/arcadia/solomon/web
andreyst-osx:web andreyst$ svn diff
Index: package.json
===================================================================
--- package.json    (revision 8554852)
+++ package.json    (working copy)
@@ -71,7 +71,7 @@
     "storybook": "start-storybook -p 9001 -s public"
   },
   "homepage": "/admin",
-  "proxy": "http://localhost:5540",
+  "proxy": "http://solomon-prestable.yandex.net",
   "babel": {
     "presets": [
       "react-app"
Index: src/api/http.js
===================================================================
--- src/api/http.js (revision 8554852)
+++ src/api/http.js (working copy)
@@ -53,7 +53,7 @@
 
 function getAuthHeaders() {
   if (isAsUserAuth()) {
-    return { Authorization: `AsUser ${Auth.state.login()}` };
+    return { Authorization: 'OAuth AQAD-xxxxxx' };
   }
 
   return {};
```

### Testing

```bash
$ make test
```

### Analyzing
```bash
$ make build
$ make analyze
```

### Storybook

```bash
$ make storybook
```

### Code quality

```bash
$ make lint
```

### Deployment

> Please check that you build code using Node.js 8.15.

1. Upload dependencies to Sandbox (if needed):
   * run ```$ make get-deps``` if ```node_modules``` doesn't exist
   * get token from Sandbox: [https://sandbox.yandex-team.ru/oauth](https://sandbox.yandex-team.ru/oauth)
   * run ```$ SANDBOX_TOKEN=<token> make upload-deps```
   * copy created resource id
   * update resource id in ```ya.make``` and commit it:  
     ```FROM_SANDBOX(FILE <RESOURCE_ID> OUT node_modules.tar.gz)```
2. Run deployment in [simcity.yandex-team.ru](https://simcity.yandex-team.ru)
