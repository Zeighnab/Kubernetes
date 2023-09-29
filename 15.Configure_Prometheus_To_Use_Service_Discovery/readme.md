### Service discovery is a mechanism by which services discover each other dynamically without the need for hard coding IP addresses or endpoint configuration

### Kubernetes service discovery is an abstraction that allows an application running on a set of Pods to be exposed as a network service. This enables a set of Pods to run using a single DNS name, and allows Kubernetes load balancing across them all. This way as Pods are dynamically created and destroyed on demand, frontends and backends can continue to function and connect


## Tasks:

* Elevate your permissions to root. Execute ./bootstrap.sh to complete the setup of the environment.

* Edit `prometheus-config-map.yml` to create two service discovery targets.

* Create a job called kubernetes-apiservers.

* The role should be set to `endpoint` and the scheme should be set to `https`.

* Configure tls_config to use `/var/run/secrets/kubernetes.io/serviceaccount/ca.crt` as the CA file, and `/var/run/secrets/kubernetes.io/serviceaccount/token` on the bearer token file.

* Relabel: `__meta_kubernetes_namespace, __meta_kubernetes_service_name, and __meta_kubernetes_endpoint_port_name`.

* Make sure these source labels are `kept`, and set `default`, `kubernetes`, and `https` for the RegEx.

* Create a second job called `kubernetes-cadvisor`.

* Set the scheme to `https`.

* Configure tls_config to use `/var/run/secrets/kubernetes.io/serviceaccount/ca.crt` as the CA file and `/var/run/secrets/kubernetes.io/serviceaccount/token` on the bearer token file.

Set the role to `node`.

* Configure three relabel settings:

* Create a labelmap that will remove `__meta_kubernetes_node_label_` from the label name.

* Create a target label that will replace the address with `kubernetes.default.svc:443`.

* Finally, create a target label that will replace the metrics path with `/api/v1/nodes/${1}/proxy/metrics/cadvisor` and set the `__meta_kubernetes_node_name` source label as the value of `${1}`.

* Reload the Prometheus pod by deleting it.

* Verify that two service discovery endpoints are appearing as targets.

![](./img/Prometheus%20labs%20-%20Lab1.png)