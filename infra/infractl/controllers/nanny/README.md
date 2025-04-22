Nanny Service controller
=======================

Features
--------

Controller translate nanny service specs from k8s to Ya.Deploy MultiClusterReplicaSet.

Building
--------

Controller is made using [kubebuilder] framework, but it is being compiled with Arcadia.

Thus it utilizes two build systems. First one is common Makefile for code-generation and
kubebuilder tools, and second one is `ya make` for building controller itself.

#### Resource definitions

To build OpenAPI spec, you'll also need .go files for YP proto resource definitions:

    arcadia$ ya make --replace-result --add-result .go yp/go/proto
    arcadia$ ya make --replace-result --add-result .go yp/go/yp
    arcadia$ ya make --replace-result --add-result .go infra/nanny/go/proto/nanny_repo

Then you can build OpenAPI spec:

    arcadia/infra/infractl/controllers/nanny$ ya make --add-result .crd.yaml --add-result .go --replace-result api

And then create spec in k8s cluster:

    arcadia/infra/infractl/controllers/nanny$ kubectl create -f api/runtime/proto_v1/nannyruntime_types.crd.yaml

Or replace if it already exists:

    arcadia/infra/infractl/controllers/nanny$ kubectl replace -f api/runtime/proto_v1/nannyruntime_types.crd.yaml

All these steps are needed only if you change CRD spec (`api/runtime/proto_v1/nannyruntime_types.proto`),
or if you apply spec to a new k8s cluster.

#### Controller

Controller can be built with:

   arcadia/infra/infractl/controllers/nanny$ ya make 

Running
-------

To run controller locally you need to provide robot OAuth token for YP:

    $ export YP_TOKEN=AQAD-...

    # or

    $ mkdir -p $HOME/.yp
    $ echo "AQAD-..." > $HOME/.yp/token

Then edit config to respect your cluster configuration:

    arcadia/infra/infractl/controllers/nanny$ vim config/manager/controller_manager_config.yaml

And run controller with:

    arcadia/infra/infractl/controllers/nanny$ ./deploy_controller -zap-devel -config config/manager/controller_manager_config.yaml

Pushing object to k8s
---------------------

Edit sample resource definition:

    arcadia/infra/infractl/controllers/nanny$ vim config/samples/nanny_v1_nannyruntime.yaml

and apply it:

    arcadia/infra/infractl/controllers/nanny$ kubectl apply -f config/samples/nanny_v1_nannyruntime.yaml
