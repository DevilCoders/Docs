# Building & deploying Abt usersplit lib

### Step 0: prerequisites

 - ya tool
 - tar
 - zip
 - maven
 - python3

### Step 1: build

For debug purposes, you can check out Arcadia, make some code modifications, and then build Arcadia package locally:

`ya package bindings/java/abt/abt-native/android/package.json`

Alternatively, you can build single .so locally:

`ya make -r --lto -DSTRIP --target-platform=DEFAULT-ANDROID-ARMV7A`

But for production you must build the package on Sandbox (revision is a commit number from Arcadia):

`python3 ./build.py --revision 1234567`

After this stage, there should be a file called somthing like `abt.r1234567.tar.gz`.

### Step 2: deploy

Deployment to the Artifactory:

`./deploy.sh abt.r1234567.tar.gz 0.1.4`

Here, the 1st argument is path to the package, built by the first step; and the 2nd argument is
 desired artifact version.
