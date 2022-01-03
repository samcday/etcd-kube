# etcd-kube

A reasonably simple set of Kubernetes manifests that deploy a 3 node etcd cluster.

The cluster is fully secured with TLS traffic, both between the cluster peers, and from clients. The certificates are managed by [cert-manager][cert-manager].

It is also monitored using the Prometheus alerting rules provided [upstream](https://etcd.io/docs/v3.5/op-guide/monitoring/#alerting).

Finally, a dashboard is setup using the [provided](https://etcd.io/docs/v3.5/op-guide/monitoring/#grafana) sample Grafana dashboard.

## Assumptions

Your cluster has the following installed:

 * [cert-manager][cert-manager]
 * [prometheus-operator](https://prometheus-operator.dev/)
 * Grafana (with the dashboard sidecar enabled)
 * [openebs-localpv-hostpath](https://openebs.io/docs/user-guides/localpv-hostpath), but you can change the storageClass to whatever you want.

## Caveats

* **The peer certificate is shared between all 3 nodes.** This is suboptimal, but really if an attacker got hold of this private key and joined a naughty etcd peer to your cluster, that implies they've already burrowed deep inside your cluster and you're likely fucked anyway? But I'm no security expert, of course.

[cert-manager]: https://cert-manager.io/
