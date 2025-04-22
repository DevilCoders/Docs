### Integration tests
We have a couple of long running computational heavy tests. Typcally we use folder name "it" for this kind of tests.
You can run them using following command:
```sh
ya make -trAP --test-stderr --keep-temps -v --test-param=run_with_yt --test-traceback=long 
```
If you see that after your changes some tests failed and you see diff on the screen you need to make sure that the changes are corresponds to your changes and canonize the changes using following command:
```sh
ya make -trAP --test-stderr --keep-temps -v --test-param=run_with_yt --test-traceback=long -Z
```
And also you need to commit the changes.
