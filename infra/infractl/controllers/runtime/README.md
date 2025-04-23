Runtime controller
=======================

Features
--------

Controller creates corresponding deploy primitives from runtime specs.

Building
--------

#### Resource definitions

To build OpenAPI spec, you'll need .go files for YP proto resource definitions:

    arcadia$ ya make --replace-result --add-result .go yp/go/proto
    arcadia$ ya make --replace-result --add-result .go yp/go/yp

Then you can build OpenAPI spec:

    arcadia/infra/infractl/controllers/runtime$ ya make --add-result .crd.yaml --add-result .go --replace-result

And then create spec in k8s cluster:

    arcadia/infra/infractl/controllers/runtime$ kubectl create -f api/proto_v1/runtime_types.crd.yaml

Or replace if it already exists:

    arcadia/infra/infractl/controllers/runtime$ kubectl replace -f api/proto_v1/runtime_types.crd.yaml

Note: kubectl apply does not work as it creates additional annotation and it is too large for Runtime.

All these steps are needed only if you change CRD spec (`api/proto_v1/runtime_types.proto`),
or if you apply spec to a new k8s cluster.

#### Controller

Controller can be built with:

    arcadia/infra/infractl/controllers/runtime$ ya make 

Running
-------

To run controller locally you need to provide robot OAuth token for YP:

    $ export YP_TOKEN=AQAD-...

    # or

    $ mkdir -p $HOME/.yp
    $ echo "AQAD-..." > $HOME/.yp/token

Then edit config to respect your cluster configuration:

    arcadia/infra/infractl/controllers/runtime$ vim config/manager/controller_manager_config.yaml

And run controller with:

    arcadia/infra/infractl/controllers/runtime$ ./runtime_controller -zap-devel -config config/manager/controller_manager_config.yaml

Pushing object to k8s
---------------------

Edit sample resource definition:

    arcadia/infra/infractl/controllers/runtime$ vim config/samples/deployinfra_v1_runtime.yaml

and apply it:

    arcadia/infra/infractl/controllers/runtime$ kubectl apply -f config/samples/deployinfra_v1_runtime.yaml
