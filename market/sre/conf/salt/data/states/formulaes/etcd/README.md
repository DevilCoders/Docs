# market-etcd-formula
To start new cluster, add pillar etcd_initial_cluster:

`salt -N market_etcd-stable-DC state.sls formulaes.etcd pillar='{"etcd_initial_cluster": true}'`


*THIS WILL BREAK EXISTING CLUSTER*
