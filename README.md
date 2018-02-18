<p align="center"><img src="https://github.com/ashleymcnamara/gophers/blob/master/KUBERNETES_GOPHER.png" width="400"></p>

<p align="center"><b>Configuring ElasticSearch logging for your Kubernetes cluster.</b></p>

# Intro #

> This course is a part of series of Kubernetes articles located at [ScalableSystemDesign]

`kubectl` and `ansible` must be installed beforehand. 

Playbooks here will help you install logging using ElasticSearch for your Kubernetes cluster.

It will install latest ElasticSearch, Kibana (with X-Pack disabled), Fluentd, collect data from your containers, 
journald (playbooks are meant for CentOS 7 servers).

| Software        | Version      |
| --------------- |--------------|
| ElasticSearch   | 6.1.2        |
| Kibana          | 6.1.2        |

Kubana configuration:

```yaml
xpack.graph.enabled: false
xpack.ml.enabled: false
xpack.monitoring.enabled: false
xpack.reporting.enabled: false
xpack.security.enabled: false
xpack.watcher.enabled: false
```

## Installing

```bash
ansible-playbook install.yaml -e 'kubeconfig=admin.conf' --extra-vars='{"nodes": [node1,node2]}' -v
```

Nodes `node1` and `node2` will be labeled with `beta.kubernetes.io/fluentd-ds-ready=true`.

## Deleting
```bash
ansible-playbook delete.yaml -e 'kubeconfig=admin.conf' --extra-vars='{"nodes": [node1,node2]}' -v
```

## References

Sources used while working on this repository:
1. [https://github.com/kubernetes-incubator/kubespray/tree/master/roles/kubernetes-apps/efk/fluentd]
2. [https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/fluentd-elasticsearch]
3. [https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/]
4. [https://github.com/reevoo/fluent-plugin-systemd]

[ScalableSystemDesign]: https://scalablesystem.design/lesson/kubernetes-logging-elk/
[https://github.com/kubernetes-incubator/kubespray/tree/master/roles/kubernetes-apps/efk/fluentd]: https://github.com/kubernetes-incubator/kubespray/tree/master/roles/kubernetes-apps/efk/fluentd
[https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/fluentd-elasticsearch]: https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/fluentd-elasticsearch
[https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/]: https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/
[https://github.com/reevoo/fluent-plugin-systemd]: https://github.com/reevoo/fluent-plugin-systemd
[https://scalablesystem.design/lesson/kubernetes-logging-elk/]: https://scalablesystem.design/lesson/kubernetes-logging-elk/