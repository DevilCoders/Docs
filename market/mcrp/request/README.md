1. replace PROJECTS_PATH and ARCADIA_PATH with real paths

2. Setup IDEA project:
    ```shell script
    cd PROJECTS_PATH/mcrp-request
    ya ide idea --directory-based --group-modules=tree --iml-in-project-root --with-content-root-modules -r . ARCADIA_PATH/market/mcrp/request
    cp PROJECTS_PATH/mcrp-request/out/production/mcrp-request/local/example.properties PROJECTS_PATH/mcrp-request/out/production/mcrp-request/local/application.properties
    ```

3. Update `PROJECTS_PATH/mcrp-request/out/production/mcrp-request/local/application.properties` with local values

4. IDEA run params:
    ```
    Main class: ru.yandex.market.mcrp_request.McrpRequest
    VM options: -Djava.library.path=PROJECTS_PATH/mcrp-request/dlls -Djna.library.path=PROJECTS_PATH/mcrp-request/dlls
    Working directory: PROJECTS_PATH/mcrp-request
    Environment variables: PROPERTIES_DIR=out/production/mcrp-request/
    Use classpath of module: mcrp-request
    ```
