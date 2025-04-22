# ExcludeDoclet

## What is this?
This is a doclet used by Javadoc in order to exclude unwanted classes and fields (they are marked with @exclude tag).
It is generally located in the Mapsmobi Maven repo.

## Where is it used?
https://a.yandex-team.ru/arc/trunk/arcadia/build/scripts/gen_aar_gradle_script.py?rev=r8672694#L210

## How do I update and build it?
```
mkdir build
javac -d ./build -classpath /Library/Java/JavaVirtualMachines/jdk<version, e.g. 1.8.0_211>.jdk/Contents/Home/lib/tools.jar *.java && cd build && jar cvf exclude-doclet-1.0.0.jar *
mv exclude-doclet-1.0.0.jar <unpacked_mapsmobi_maven_repo>/com/yandex/android/javadoc/exclude-doclet/<version>/exclude-doclet-<version>.jar)
```
Now make any changes you need in the Maven repo, then upload it as usual. Don't forget to change the version (or possibly insert a wildcard) [here](https://a.yandex-team.ru/arc/trunk/arcadia/build/scripts/gen_aar_gradle_script.py?rev=r8672694#L213)

## Where did it come from? Should we worry about copyright?
Probably definitely not. The author states so (almost) explicitly [on a long forgotten and currently unavailable page](https://web.archive.org/web/20171228054820/http://www.sixlegs.com/blog/java/exclude-javadoc-tag.html)
