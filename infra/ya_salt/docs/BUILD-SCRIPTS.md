# Image build scripts
Hostmanager could be used during porto/vm image builds.
For such purpose ya-salt has special `apply` command.
`ya-salt apply` command accepts spec file with `kind: BuildScriptSpec`.

Example of invocation:
`ya-salt apply -f <path-to-spec.yaml>`

## BuildScriptSpec format
    meta:
      kind: BuildScriptSpec
      name: <spec name>
    spec:
      saltenv: <saltenv to look for top.sls>
      roots:                            # definition of file_roots to look up states/jinja files
        - <first file_root, usually same as saltenv>
        - <file root 2>
        ...
        - <file root N>
      # one of
      path: ./saltstack                 # path to salt states repo root
      # or
      server:                           # hm-servers definition
        hosts:
          - hm-server-fqdn1
          - hm-server-fqdn2
          ...
          - hm-server-fqdnN
### Example configs used for testing
    # app.yaml
    meta:
      kind: "BuildScriptSpec"
      name: app-images
    spec:
      saltenv: app-image
      roots:
        - app-image
        - images-include
        - common
      path: /home/warwish/saltstack

    # os-sub.yaml
    meta:
      kind: "BuildScriptSpec"
      name: os-sub-image
    spec:
      saltenv: os-sub-image
      roots:
        - os-sub-image
        - images-include
        - common
      path: /home/warwish/saltstack

    # os.yaml
    meta:
      kind: "BuildScriptSpec"
      name: os-image
    spec:
      saltenv: os-image
      roots:
        - os-image
        - images-include
        - common
      path: /home/warwish/saltstack

    # vm.yaml
    meta:
      kind: "BuildScriptSpec"
      name: vm-image
    spec:
      saltenv: vm-image
      roots:
        - vm-image
        - images-include
        - common
      path: /home/warwish/saltstack
