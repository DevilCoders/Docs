# kubectl-yandex

This is kubectl plugin: https://kubernetes.io/docs/tasks/extend-kubectl/kubectl-plugins/

To make it work:

* Build plugin with ya-make
* Move binary to PATH
* Now plugin available as `kubectl yandex`

# Features:

* `kubectl yandex auth` Exchange ssh key to yandex OAuth token
* ~~WIP: `kubectl yandex config` Add yandex kubernetes cluster with CA and address in ~/.kube/config~~
