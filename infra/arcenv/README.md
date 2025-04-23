# arcenv

Prepare environment for local running your Ya.Deploy contoller.

Sometimes Ya.Deploy service has multiple env-variables including some secrets, 
and one has to perform multiple actions to bootstrap it for local run.
Moreover, it often requires to maintain the set of that variables in sync with
Ya.Deploy configuration.

To help with that I wrote this little helper. It allows you to just make YAML-file
pointing at your service in Ya.Deploy, and it will instantiate all the same
variables as your workload would receive.


## How to use

1. Build arcenv with:

        ya make -rE --dist infra/arcenv

2. Add it to your ``PATH``, e.g. if you have ~/bin in your ``PATH``, you can just do:

        cp -r infra/arcenv/arcenv ~/bin/

3. Write ``env.yaml`` in the root of your project. It has the following structure:

        stage: my_stage
        deploy_unit: my_du
        box: my_box
        # optional field, if not present workload env variables would not be present
        workload: my_workload
        # optional field, by default xdc is used
        cluster: xdc
        # optional dict to add/override some variables
        custom_env:
            var1: "val1"
            var2: 1234


4. Exec in the root of your project:

        eval $(arcenv)

    Optionally you can specify custom path to spec if you store it elsewhere:

        eval $(arcenv --env /path/to/env.yaml)

5. Now you are probably ready to run your service locally.


## How it works

arcenv uses the same OAuth token as dctl, to retrieve stage spec from Ya.Deploy
and find all the variables needed.

It then resolves the secrets required in the Ya.Vault and prints corresponding POSIX shell commands
to set all the environment variables. Invoking ``eval`` over its output calls these commands.

From the above it is implicitly presumed that you must have permissions in Ya.Vault to read all the
secrets required.
