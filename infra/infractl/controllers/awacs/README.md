Awacs configuration controller
===============================

Features
--------

Controller configures awacs entities.

Building
--------

#### Resource definitions

To build OpenAPI spec:

    arcadia/infra/infractl/controllers/awacs$ ya make --add-result .crd.yaml --add-result .go --replace-result

And then create spec in k8s cluster:

    arcadia/infra/infractl/controllers/awacs$ kubectl create -f api/upstream/proto_v1/awacsupstream_types.crd.yaml

Or replace if it already exists:

    arcadia/infra/infractl/controllers/awacs$ kubectl replace -f api/upstream/proto_v1/awacsupstream_types.crd.yaml

All these steps are needed only if you change CRD spec (`api/*/proto_v1/*.proto`),
or if you apply spec to a new k8s cluster.

#### Controller

Controller can be built with:

    arcadia/infra/infractl/controllers/awacs$ ya make

Running
-------

    arcadia/infra/infractl/controllers/awacs$ ./awacs_controller  -config config/manager/controller_manager_config.yaml
