# How to create Pandora gun shooting via gRPC
1. Install [Go](https://golang.org/doc/install)
2. Install [Pandora](https://github.com/yandex/pandora)
3. Compile grpc service's proto files
    - Install protoc
        ```
        $ export GO111MODULE=on  # Enable module mode
        $ go get github.com/golang/protobuf/protoc-gen-go
        ```
    - Compile with protoc
        ```
        make protoc
      ```
4. Build Go modules You should have two modules: one for **gun** and one for your compiled **proto files**.
    - To build proto module use:
    ```
    cd spamalot/spamlot_proto
    go build
    ```

   There can be some problems with go modules, but it should get you the command to install them

    - To build gun module:
   ```
   cd ../..
   go build
    ```
5. Local test
    - load.yaml is config for pandora gun you can tweak it as you wish
    - create ammo.json
        ```
      cd ammo-gen
      go build
      ./ammo-gen
      ```
    - run ./gun
6. Shoot via YandexTank
    - build your gun for Xenial
    ```go
    env GOOS=linux GOARCH=amd64 go build
    ```
    - upload your gun and ammo somewhere where tank can get it. You can use [Firestarter](https://lunapark.yandex-team.ru/firestarter/)
    - create custom config for Firestarter. It will contain your local config in **config_content** section and urls for uploaded gun and ammo in **pandora_cmd** and **resources** sections
    ```yml
    phantom:
      enabled: false
      address: 'lb-int-01-myt.test.vertis.yandex.net:80'
    pandora:
      pandora_cmd: 'https://storage-int.mds.yandex.net/get-load-ammo/21373/e3d120f3984743a6a0127502dc17356f'
      enabled: true
      expvar: false
      resources:
        - src: 'https://storage-int.mds.yandex.net/get-load-ammo/29344/654b51eee8a34592a65c964320a28568'
          dst: ./ammo.json
      config_content:
        pools:
          - id: grpc_pandora_gun # pool name (for your choice)
            gun:
              type: grpc_pandora_gun  # custom gun name specified
              target: "lb-int-01-myt.test.vertis.yandex.net:80" # tank will not shoot balancer
              balancer: "spamalot-api-grpc-api.vrts-slb.test.vertis.yandex.net"
            ammo:
              type: custom_provider
              source:
                type: file
                path: ./ammo.json
            result:
              type: phout
              destination: ./phout.log
            rps: {duration: 30s, type: line,  from: 1, to: 10}
            startup:
              type: once
              times: 10
        log:
          level: error
    uploader:
      enabled: true
      job_dsc: ""
      job_name: ""
      operator: kusaeva # staff name
      task: VSDATA-827
      ver: ""
    ```


