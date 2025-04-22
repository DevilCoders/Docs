Roles configuration  controller
===============================

Features
--------

Controller configures RBAC objects in namespace.

Building
--------

#### Resource definitions

To build OpenAPI spec, you'll need .go files for YP proto resource definitions:

    arcadia$ ya make --replace-result --add-result .go yp/go/proto
    arcadia$ ya make --replace-result --add-result .go yp/go/yp

Then you can build OpenAPI spec:

    arcadia/infra/infractl/controllers/roles$ ya make --add-result .crd.yaml --add-result .go --replace-result

And then create spec in k8s cluster:

    arcadia/infra/infractl/controllers/roles$ kubectl create -f api/proto/rolesconfiguration_types.crd.yaml

Or replace if it already exists:

    arcadia/infra/infractl/controllers/roles$ kubectl replace -f api/proto/rolesconfiguration_types.crd.yaml

All these steps are needed only if you change CRD spec (`api/proto/rolesconfiguration_types.proto`),
or if you apply spec to a new k8s cluster.

#### Controller

Controller can be built with:

    arcadia/infra/infractl/controllers/roles$ ya make

Running
-------

    arcadia/infra/infractl/controllers/roles$ ./roles_controller
