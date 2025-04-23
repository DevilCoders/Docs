## Local debugging

### Prerequisites

1. You have `ya` tool installed and exists in your PATH: [Arcadia quick start](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#ya-setup)
2. You have `tvmtool` installed and exists in your PATH. The easiest way to install is pypi: [How to install tvmtool from pypi](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#izpypi)
3. tvmtool with environment variables configured

### Tvmtool configuration

1. Create tvmtool configuration:
    ```
    tvmtool add_only_for_check --tvmid 2033817:gallifrey-test
    tvmtool setport -p 33333
    ```
2. Run tvmtool to generate auth_token: `tvmtool -u`
3. Find next strings:
    ```
    WARN	Auth token isn't set by user, it will be generated automatically
    WARN	Server access token: b24ff68edb9dc6c555fc1ae88d23c926
    ```
4. Stop tvmtool with Ctrl+C
5. Set up `TVMTOOL_LOCAL_AUTHTOKEN` and `DEPLOY_TVM_TOOL_URL` environment variables. For zsh add next lines to your `~/.zshrc`:
    ```
    export TVMTOOL_LOCAL_AUTHTOKEN=b24ff68edb9dc6c555fc1ae88d23c926
    export DEPLOY_TVM_TOOL_URL=http://localhost:33333
    ```
6. Restart your shell
7. Launch tvmtool: `tvmtool -u`
8. If output contains string `DEBUG Got authtoken from TVMTOOL_LOCAL_AUTHTOKEN` then tvmtool configured correctly

### Debugging

{% note info %}

Every commands are executed from Arcadia mount root

{% endnote %}

1. Generate service ticket for unit-testing: `ya tool tvmknife unittest service -s 2033817 -d 2033817`
2. Launch tvmtool for unit-testing: `tvmtool -u`
3. Complile grpc_client: `ya make apphost/tools/grpc_client`
4. Create context file `~/context.json`:
    ```json
    {
        "tvm-ticket": "<service ticket from #1>",
        "answers": [
            {
                "name": "INIT",
                "results": [
                    {
                        "type": "<type from proto (typing_apphost_type)>",
                        "__content_type": "json",
                        "binary": {
                            <request params in json>
                        }
                    }
                ]
            }
        ]
    }
    ```
5. Run your application (from IDE or from shell). Default port: 10000
6. Run grpc_client: `apphost/tools/grpc_client/grpc_client -f ~/context.json localhost:10000/<path from proto service (option(path))>`
